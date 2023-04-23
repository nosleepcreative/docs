---
description: Proceduralism
---

# Techniques

## Readings

* [https://www.deborahrfowler.com/HoudiniResources/HoudiniOverview.html](https://www.deborahrfowler.com/HoudiniResources/HoudiniOverview.html)

## Transferring attributes

* Using `attribtransfer` eg. P, Cd
* Using Pointwrangle Get attributes from second input in wrangle node \[[src](https://www.sidefx.com/forum/topic/54084/)]

&#x20;If you want to get an attribute (lets say color) from a specific point number (lets say 123456) from input 2, you can use

```
@Cd = point(1, 'Cd', 123456);
```

If you have the same number of points on both inputs and you want to get an attribute from the corresponding point on input 2 you can use this shortcut

```
@Cd = v@opinput1_Cd;
```

Where the number 1 describes the input port.



&#x20;Ah, you want the number of points on input 1?\


```
@number_of_points_on_input_1 = npoints(1)
```

## Copy stamping & Looping

* [Looping](https://www.deborahrfowler.com/HoudiniResources/Overview-Looping.html), Deborah Fowler

There are three ways of manipulating and copying points

1. `Copy Stamp` with Expressions - good for quick prototyping
2. `Copy to Points` with a SOP eg. `circle`
3. `Copy to Points` with `pointwrangle` and VEX

###

## Point generation&#x20;

1. Using VEX
2. Using `line` to create points > `point` to change the position eg. Creating circle of points

## Orient objects or profiles to a curve

### Using polyframe

## Instancing = packed geo & copypoints

#### Tutorials

* [https://vimeo.com/207724703](https://vimeo.com/207724703)

### Lights&#x20;

* `Instance` - similar to copytopoints to grid
  * Select Instance object
  * Place points or geo inside network
  * Point Instancing: Fast-point for geometry, **full point instancing** for lights&#x20;

### **Random geometries**

* Pros: faster processing and work with render engines
* Reveal instance in viewport via Display Opetion > Geometry > Instancing

1. create mmultiple objects: demo1, demo2, demo3
2. attribcreate -&#x20;
   1. string , name: "instance", String: /obj/demo1
   2. /obj/demo\`round(fit01(rand(@ptnum),1,2))\`

![](<../../.gitbook/assets/image (6).png>)

### **Random geometry with copytoPoints**

* **Attach an attribute called "variant"  to each geometry**

1. geometry eg. object\_merge > pointWrangle - `i@variant =1;`

#### Generating a random integer value for each point&#x20;

* **grid>** attribrandomize - scale > point wrangle

```
int(rint@variant = fit01(rand(@ptnum),0,2));
```

* **Retrieve the random variable values  by listing "variant" in the Piece Attrbute from  copytopoints**&#x20;
* transform using target point orientation
* Setting the object to faceup: pointwrangle: @N = {1,0,0};

#### Unpacking

* Arnold renderer does not accept pack**ed** geo
* add `unpack`

## Texturing

### Random color ovveride

```c
// rand bw color
rand(@ptnum), rand(@ptnum), rand(@ptnum)
// rand RGB
rand(@ptnum) , rand(@ptnum+25), rand(@ptnum+10)
```

## Multi-image texturing

* [Texture Override](https://www.deborahrfowler.com/HoudiniResources/HoudiniTipsAndTricksRender.html), Deborah Fowler
* [Light Instancing](https://www.deborahrfowler.com/HoudiniResources/Lights-Instanced.html), Deborah Fowler

### Using copy stamp and expressions

Prerequisite: You must use an image sequence; eg. all files are named: image\_04.jpg

1. Assign  a `material` SOP and input a principle shader to target object
2. Activate `Overrides use Local overrides` and `merge Ove`r`rides`
   1. Parameter: **basecolor\_texture**
   2. Use any of these expressions: &#x20;

```c
// using frame number
$HIP/textures/image_$F2.png

// random image from concatenating strings
$HIP/textures/image_`padzero(2,ceil(fit01(rand(@ptnum),0,7)))`.png
$HIP/tex/`image_floor(fit01(rand(@primnum),0,90))`.png

// Use all of your sequence frames: 
$HIP/tex/`image_@primnum%90`.jpg

```

* 90 is an arbituary value ; you can use your total image sequence frames
* &#x20;the **backticks \`** allows use to add an expression into the string
* This technique is similar to copyStamp; we are referencing primnumber and adding an different image for  each.

### Texture override

**CopyPacked geo**

* grid with uvproject1
* expression in material node (point attrib)

**CopyUnpacked**

* stamp input
* material

### Method: based on frame number

1. copy stamp
2. material&#x20;
   1. parameter: basecolor\_texture
   2. type: string value
3. String value:

### Based on UV&#x20;

Pros: good for seamless tiling eg. brick tesselattion&#x20;

1. grid > uvproject > group > material

### Based on luminance value

* [https://forums.odforce.net/topic/29212-texture-on-copy-based-on-luminance-value/](https://forums.odforce.net/topic/29212-texture-on-copy-based-on-luminance-value/?do=findComment\&comment=165461)

## Texturing & UV

### Best practice for assigning materials

* Texturing prim faces with the same image using groups: [https://www.deborahrfowler.com/HoudiniResources/Overview-UVs.html](https://www.deborahrfowler.com/HoudiniResources/Overview-UVs.html)
* polygon sop >  `uvproject`
  * `uvquickshade`

## Recursive subdivision

Space partitioning algorithm

### Tutorials:

* [Loops & VEX: Artistic Quadtrees](https://youtu.be/uN8Kxxvpkzc), Entagma
* [Spiral Pattern Generation Tutorial - Houdini + Cinema4D](https://www.youtube.com/watch?v=ZHgzif3iIzY), Roman Pillai



## Unsorted VEX notes

### Torus wrangle node example

```c
// bbox equivalent 
@Cd.r = relbbox(0,@P).x;
@Cd.g = relbbox(0,@P).y;
@Cd.b = relbbox(0,@P).z;
```

* Using `facet` to make unique points;

### Simulating bubble popping with scatter

```c
if(@P.x>ch('threshold') + .5 * (noise(@P * 5)* 2 - 1)){
    removepoints(@ptnum)
}
```

* Sphere > Scatter > delete by threshold for pos.x
* particlefluid surace
