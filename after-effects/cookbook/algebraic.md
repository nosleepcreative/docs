---
description: 'Last update: 8 June 2021'
---

# Algorithmic

## Square&#x20;

### createPath

{% tabs %}
{% tab title="square" %}
```javascript
vertices = [[0,0], [100,0], [100,100], [0,100]];
inTangents=[]
outTangents=[]
closed = true;
createPath(vertices,inTangents, outTangents, closed);
```
{% endtab %}
{% endtabs %}

## Triangle

### createPath

```javascript
l = 100;
w = 50;
vertices = [[0,0], [-w,l], [w,l]]
inTangents=[]
outTangents=[]
closed = true;
createPath(vertices,inTangents, outTangents, closed);
```

## Circle

$$
x = radius*sin(theta)\\ y = radius*cos(theta)
$$

### createPath

* Source: [Dan Ebbert](https://forums.creativecow.net/docs/forums/post.php?forumid=227\&postid=39882\&univpostid=39882\&pview=t) — circle

{% tabs %}
{% tab title="no tangent" %}
```javascript
var pts = 50;
var a = 500; //radius
var completion = 100 / 100;

var t, x, y;
var vertices = [];

for (i = 0; i < pts; i++) {
  t = i / pts * Math.PI * 2 * completion; // element num/ num of elements ;
  x = a * Math.cos(t);
  y = a * Math.sin(t);
  vertices[i] = [x, y]
}
createPath(vertices, [], [], 1)
```
{% endtab %}

{% tab title="w/ tangent" %}
```javascript
w = 500; // width
r = w/2;
ratio = .5523;
t = r*ratio;
vertices = [[r,0],[0,r],[r,2*r],[2*r,r]];
inTangents = [[t,0],[0,-t],[-t,0],[0,t]];
outTangents = [[-t,0],[0,t],[t,0],[0,-t]];
createPath(vertices,inTangents,outTangents,1);
```
{% endtab %}
{% endtabs %}

## [Eight curve](https://mathworld.wolfram.com/EightCurve.html)

$$
x= a *sin(t)\\y=asin(t)cos(t)
$$

### Position

```javascript
// source: Dan Ebbert

center = [thisComp.width,thisComp.height]/2;
radius = 200;
period = 3;
angle = 2*Math.PI*time/period;
x = 2*radius*Math.cos(angle)*Math.sqrt(Math.cos(angle)*Math.cos(angle));
y = 2*radius*Math.cos(angle)*Math.sin(angle);
center + [x,y]
```

## Torus

$$
x=(a+bcosu)cosv 
\\
y=(a+bcosu)sinv\\
z=bsinu
$$

### Position

```javascript
u = 1
v = 2
a = 540;

x = a*Math.cos(v*time)*Math.sin(u*time);
y = a*Math.cos(v*time)*Math.cos(u*time);
[x,y]+[thisComp.width/2,thisComp.height/2]
```

### createPath

```javascript
var pts = 50;
var u = 1
var v = 10;
var a = 75 // inner radius
var c = 450 // outer radius
var completion = 100 / 100;

var t, x, y;
var vertices = [];

for (i = 0; i < pts; i++) {
  t = i / pts * Math.PI * 2 * completion; // element num/ num of elements ;
  x = (c + a * Math.cos(v * t)) * Math.cos(u * t);
  y = (c + a * Math.cos(v * t)) * Math.sin(u * t);
  vertices[i] = [x, y]
}
createPath(vertices, [], [], 1)
```

## Wavy Circle

### Position

```javascript
u = 1
v = 10;
a = 75 // inner radius
c = 450 // outer radius
phase = 10; // animate this


x = (c+a*Math.cos(v*phase))*Math.cos(u*phase);
y = (c+a*Math.cos(v*phase))*Math.sin(u*phase);
[x,y]+[thisComp.width/2,thisComp.height/2]
```

## Conical spiral (equidistant)

### Position

```javascript
freq = 60;
mul = 500;
radius = 90;

x = radius*Math.sin(time*freq)
y = radius*Math.cos(time*freq)
z = time*mul
value  + [x,y,z]
```

## Archimedes Spiral

* [**Polar Coordinates in Houdini | VEX Quickies**](https://www.youtube.com/watch?v=hgEcnfyBvf8)**, David Kahl**

### createPath

{% tabs %}
{% tab title="path property" %}
```javascript
// connect to sliders
let w = 1000;
let points = 200;
let steps = 20;
let angle = 0;

let r = w / 2;
let step = (Math.PI * 2) / steps;
let radius = 0;
let vertices = [];

//main
for (i = 0; i < points; i++) {
    angle += step;
    radius = i / points * r;
    x = Math.cos(angle) * radius;
    y = Math.sin(angle) * radius;
    vertices[i] = [x, y];
}

createPath(vertices, [], [], 0)
```
{% endtab %}
{% endtabs %}

## Phyllotaxis&#x20;

### Position

```javascript
var a = 137.508;
var r = 25; 

var theta = degreesToRadians(myIndex * a);
var myIndex = index - thisComp.layer("controls").index;

x = r * Math.sqrt(myIndex) * Math.cos(theta);
y = r * Math.sqrt(myIndex) * Math.sin(theta);

[x, y] + [thisComp.width, thisComp.height] / 2;
```

## Harmonic Motion

### createPath

{% tabs %}
{% tab title="sine" %}
```javascript
// var ctrl = thisLayer;
var inc = 1500;
var amp = 300;
var n = 30;
var freq = .5
var seed = 185;

var vertices = [];
var x, y, pt, phase;
seedRandom(seed, true)
var offset = random() * Math.PI * 2

for (i = 0; i < n; i++) {
  pt = i / (n - 1);
  x = inc * pt

  phase = time * freq * Math.PI * 2 + pt * Math.PI
  //phase += offset;

  y = amp * Math.sin(phase);
  //y *= Math.sin(phase / 2);
  //y *= Math.sin(phase / 3);
  //y += noise(time + pt) * 100;

  // create point
  vertices[i] = [x, y]
}

createPath(vertices, [], [], 0)
```
{% endtab %}

{% tab title="squiggly" %}
```javascript
// var ctrl = thisLayer;
var inc = 1500;
var amp = 300;
var n = 50;
var freq = .5
var seed = 185;
var r = 0.25;


var vertices = [];
var x, y, pt, phase;
seedRandom(seed, true)
var offset = random() * Math.PI * 2

for (i = 0; i < n; i++) {
  pt = i / (n - 1);
  x = inc * pt 

  phase = time * freq * Math.PI * 2 + (pt * Math.PI /r)
  // phase += offset;

  w1 = Math.sin(phase);
	y = amp * w1;

  // create point
  vertices[i] = [x, y] 
}

createPath(vertices, [], [], 0)
```
{% endtab %}
{% endtabs %}

