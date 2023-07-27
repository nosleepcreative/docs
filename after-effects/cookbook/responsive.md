# Responsive

### Carousel / Rotating layers&#x20;

![](<../../.gitbook/assets/carousel continuous.gif>)

```javascript
/*  There needs to be two layers named 'startCard' & 'endCard'
    This allows rotation value to dynamically change when layers are inserted or removed.
    All duplicates need to be placed within these two layers
*/

//anchor point
radius = 500
value+[0,0,radius]

// Y rotation

startIndex=thisComp.layer("startCard").index; 
endIndex = thisComp.layer("endCard").index;
numpt = startIndex-endIndex+1; // total number of layers
myIndex = index-startIndex;
angle = 360/numpt

myIndex*angle
```

#### Linking layers' rotation with opacity

![](../../.gitbook/assets/carousel\_opacity.gif)

{% tabs %}
{% tab title="Using distance & vector position" %}
```javascript
// Make sure there is a camera 

//Opacity
startVal = 0;
endVal = 100;
fadeAngle = 180;

v = toCompVec([0,0,1]); // layer position to comp position in Z
d = length(toWorld(anchorPoint),thisComp.layer("Camera 1").toWorld([0,0,0]));
c = v[2]/d;
ease(c,Math.cos(degreesToRadians(fadeAngle)),1.0,startVal,endVal)

```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="using rotation" %}
```javascript
angle = transform.yRotation%360;
minAngle = 0;
maxAngle = 360;
mid = (maxAngle+minAngle)/2;
if (angle < mid)
  linear(angle,minAngle,mid,100,0)
else
  linear(angle,mid,maxAngle,0,100)
```
{% endtab %}
{% endtabs %}

## Challenge: creating user-friendly controls

* Writing expressions can be easy for you but it's a complete foreign language to other people. If you pass an expression setup to your team mates, there are chances they do not know how to operate it, modify or troubleshoot or their own.
* The best practice is to create everything they need in the Effects panel without them having to change any expressions.
* Subsequently, more functionalities can be added as the user realize the limitations of your setup.

## Importance of converting to world space

* sourceRectAtTime only reads the source size and any scale change is not applied. Hence to get the correct pixel size of a layer, this is the general formula&#x20;

$$
sourceRectAtTime().width*transform.scale[0]/100
$$

## Responsive sizing text box

* Uses: Lower thirds, quotation boxes

### Method

1. Get `sourceRectAtTime` of source text layer
2. Create `Slider Controls` for X & Y padding&#x20;

### Attaching layers to corners of a quote box

![Quotation marks attached to the corners of the text box](<../../.gitbook/assets/image (37).png>)

#### Method 1: Arithmetic&#x20;

1. Get the size of the text layer using sourceRectAtTime
2. Link the position of the layer to the text position
3. Subtract or add half the size of the quotation box to get the top or bottom corner

```javascript
s = thisComp.layer("text").sourceRectAtTime();
mySize = [s.width,s.height]/2 
thisComp.layer("text").transform.position + mySize // bottom corner
```

**Method 2: Converting sourceRectAtTime to World Space**

```javascript
s = thisComp.layer("text").sourceRectAtTime();
topLeft = [s.left,s.top]; // top left corner
botRight = topLeft+ [s.width,s.height]; // bottom right corner
thisComp.layer("text").toWorld(botRight) // change variable name to switch corners
```

#### Implementation

![Retrieving all sourceRectAtTime values using animation preset](<../../.gitbook/assets/image (18).png>)

Personally, I like to **retrieve all property values and coordinates and do any necessary calculations into slider controls in a single shape layer or null control.** This way, I can just link other parameters to that one layer. The example above, I have saved all slider controls into an animation preset so I can reuse my setup without having to rewrite the expressions

### 2-liner with conditional sizing (left-aligned text)

```javascript
// null layer "controls"
    // 1. Create 2 layer controls and select text layers;
    // 2. Create 3 point controls: "heightWidth","heightWidthWithPad", "padding"


// "heightWidth" point control expression
t = effect("Layer Control")("Layer").sourceRectAtTime();
t2 = effect("Layer Control 2")("Layer").sourceRectAtTime(time - 1);
y = 50; // height of textbox 

t.width < t2.width ? [t2.width, y] : [t.width, y]

// "heightWidthWithPad" point control expression
effect("heightWidth")("Point") + effect("padding")("Point")


// Rectangle shape layer "textbox"
    // SIZE 
    thisComp.layer("controls").effect("heightWidthWithPad")("Point")

    // LAYER ANCHOR POINT
    s = sourceRectAtTime();
    [s.left,s.top] // left align
    [s.width/2,0]; // right align,right align your text layers in the paragraph panel & reposition everything as needed.


// Line 1 text justification
//Put a "Tracking" parameter text animator onto your text layer with this expression
padding = thisComp.layer("controls").effect("padding")("Point")[0];
numChar = text.sourceText.length;
padding/numChar;

// This will justify your line 1 to the textbox, provided that line 2 is shorter

```

## Shape follows typewriter

* Attach a shape layer to the end of  a type writer Text Animator on Text layer
* Or basically,  the shape always follows at the end if the written text for it to look like that shape is typing the text on screen?

The challenge is that: **sourceRectAtTime do not recognize the size change with Text Animator** that is effecting the typewriting.&#x20;

The solution is to&#x20;

* get the position of the text in world space
* the sourceRectAtTime width
* adding a padding&#x20;

$$
linear(completion,0,100, startPos,startPos+sourceRectAtTime.width
$$
