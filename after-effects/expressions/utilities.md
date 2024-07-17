# Utilities

## Accessing sub-objects

### Get layer's pixel size&#x20;

```javascript
function getSize(layer){
	var src = layer.sourceRectAtTime();
	var s = layer.transform.scale
	var size = [src.width*s[0],src.height*s[1]]/100;
	return size;
}
```

### Get layer's top left coordinates&#x20;

```javascript
function getSrcRectTopLeft(layer){
	s = layer.sourceRectAtTime();
	localPos = [s.left,s.top];
	worldPos = layer.toWorld(localPos);
	return worldPos;
}
```

### Get effect index number

```javascript
// effect index 
thisProperty.propertyGroup(1).propertyIndex;
```

### Get number of effects applied to a layer

```javascript
// referencing locally
thisLayer("ADBE Effect Parade").numProperties
thisLayer("Effects").numProperties

// referencing other layer
thisComp.layer("layer")("ADBE Effect Parade").numProperties
thisComp.layer("layer")("Effects").numProperties 

// other method
thisProperty.propertyGroup(2).numProperties
```

* [https://www.youtube.com/watch?v=xgUNncvKXY8](https://www.youtube.com/watch?v=xgUNncvKXY8)

## Working with Array

* https://dmitripavlutin.com/operations-on-arrays-javascript/

### [Shuffling elements](https://stackoverflow.com/questions/6274339/how-can-i-shuffle-an-array)

```javascript
function shuffle(a) {
    var j, x, i;
    for (i = a.length - 1; i > 0; i--) {
        j = Math.floor(Math.random() * (i + 1));
        x = a[i];
        a[i] = a[j];
        a[j] = x;
    }
    return a;
}
```

### Check how many array is empty

```javascript
const arr = [[], [1,4,5], [], [4,6,7];

// method 1: conditional -> sum
numbers.map(x=> x.length>0: 1:0).reduce((a, b) => a + b, 0) 

// method 2 
arr.filter(x => x.length>0).length // get array of true results -> length

```

### Finding minimum or maximum element

In ES6, you can use the `...` operator to spread an array and take the minimum or maximum element.

```javascript
var myArray = [1, 2, 3, 4, 99, 20];

var maxValue = Math.max(...myArray); // 99
var minValue = Math.min(...myArray); // 1
```

### Get length of each element

```javascript
// get length of each array element
elemLength = str.map(s=>s.length)
```

### [Sum of previous elements ](https://stackoverflow.com/questions/47095238/sum-of-previous-elements-from-an-array-in-javascript)

```javascript
// method 1: using mapget character index 
let array = [1,5,6,8,10],sum;
array = array.map(elem => sum = (sum || 0) + elem);

// method 2: using reduce and map
let array = [280,430,408,430,408];
array = array.map((elem, index) => array.slice(0,index + 1).reduce((a, b) => a + b));

//  best method: using double arrow functions
var array =[280, 430, 408, 430, 408]
result = array.map((s => a => s += a)(0));
result;
```

### Comparing a value to elements, filtering conditions

```javascript
let array = [1, 3, 5, 7, 10];
v = 6;

// method 1: conditional -> sum of array 
row = (array.map(c => v >= c ? 1 : 0)).reduce((a, b) => a + b, 0)

// method 2: get index of true results, then get max value
row = Math.max(...array.map(c => v>=c? array.indexOf(c):0))

// best method: filter 
row = array.filter(c => v >= c).length
```

## Increment by Index

* Usage: tiling, valueAtTime offset

```javascript
function indexInc(mainlayer, offset, randRange) {
    var startIndex = mainlayer.layer(index - 1).index
    var myIndex = index - startIndex;
    try {
        var inc = offset * random(randRange[0], randRange[0])* myIndex;
    } catch (e) {
        inc = offset * myIndex;
    }
    return inc;
}

// usage for tile y
mainLayer.transform.position + [0+indexInc(mainLayer,50]
```

## Checking selected layer

### **Shape Layer**

This snippet returns if the layer is a shape layer by checking if there is "Contents" property group.

```javascript
isShapeLayer = thisLayer.content == "Contents" ? 1 : 0;
```

## Loops

### Through every frame

```javascript
for(t = 0; t <  thisComp.duration; t = t + thisComp.frameDuration){ 
    // statements to execute
    }
```

## Unsorted

### [Convert cartesian coordinates to polar](https://creativecow.net/forums/thread/convert-cartesian-coordinates-to-polar/)

```javascript
//If you want it relative to the comp’s [0,0] (upper left corner)

[length(xyArray),radiansToDegrees(Math.atan2(xyArray[1],xyArray[0]))]
```

#### Explanation

&#x20;Using simple trigonometry:

Imagine you have the point \[960, 540];

Those 2 values, 960 and 540, represent two adjacent sides of a triangle.

Now, if you recall back to 9th Grade, you may remember that there is a simple equation to get the third side of that triangle. A² + B² = C². So, we can find the third side (the magnitude) by using an equation like:

var mag = Math.sqrt(Math.exp(position\[0], 2) + Math.exp(position\[1], 2));\
Essentially saying take the square root of X² + Y².

Fortunately, AE gives us the handy little ‘length’ operator, which simply does all of these computations for us.

—

Another similar equation can be used to find the angle of a triangle when you know two other sides, you may remember SOH CAH TOA.

Imagine the angle at the top left of your comp, now notice that you have the opposite side (the Y coord) and the adjacent side (the X coord). Since TOA uses both opposite and adjacent sides, we can get that angle using an equation like this:

```javascript
tan(theta) = opposite/adjacent
tan(theta) = 540/960
theta = tan−1(5625)

//or, in code
var angle = Math.atan(position[1] / position[0]);
var angle_deg = radiansToDegrees(angle);
```

## Null / Camera Rigs

### Add sliders with specific affix names to property&#x20;

{% tabs %}
{% tab title="expression" %}
```javascript
var n =  thisLayer("Effects").numProperties
var fxstr = "z_add"
for(i=1;i<=n;i++){
	if(effect(i).name.includes(str)){
		value+= effect(i)(1);
	}
}
```
{% endtab %}

{% tab title="function" %}
```javascript
function sliderAdd(fxName){
	n =  thisLayer("Effects").numProperties;
	for(i=1;i<=n;i++){
		if(effect(i).name.indexOf(fxName)==0){
			value+= effect(i)(1);
		}
	}
	return value;
};

sliderAdd("Slider");
```
{% endtab %}
{% endtabs %}

## Autonomous agents&#x20;

### Auto-capture ball by Aaron Cobb

```javascript
var ball = thisLayer;
var cup = thisComp.layer("Cup");

var captureDuration = .25; //time for ball to reach center of cup once capture beings
var captureRadius = 100; //radius around anchor point of cup at which ball will be captured.

var captureTime = thisComp.duration; //time at which capture begins, default to end of comp
var currentDistance;

for(t = 0; t < captureTime; t = t + thisComp.frameDuration){ //loop through frames
    currentDistance = length(ball.toComp(ball.anchorPoint.valueAtTime(t), t), cup.toComp(cup.anchorPoint.valueAtTime(t), t));
    if(currentDistance < captureRadius) captureTime = t; //if inside capture radius exit the loop
    }
    
// execute
ease(time, captureTime, captureTime + captureDuration, value, cup.toComp(cup.anchorPoint.value));
```

### Compounding ease() interpolation ([source](https://forums.creativecow.net/docs/forums/post.php?forumid=227\&postid=36351\&univpostid=36351\&pview=t))

You can't control the influence directly, but you can compound the ease such as below.&#x20;

```javascript
if (numKeys > 1){
  t1 = key(1).time;
  t2 = key(2).time;
  v1 = [0,540];  
  v2 = [1080,540];
  t = easeOut(time,t1,t2,0,1); // using a normalized value to drive the 2nd ease
  easeOut(t,0,1,v1,v2);
}else
  value
```

* **Interactive app for easing:** [**http://gizma.com/easing/**](http://gizma.com/easing/)
* [**http://robertpenner.com/easing**/](http://robertpenner.com/easing/)
* [**Ease function generator**](http://www.timotheegroleau.com/Flash/experiments/easing\_function\_generator.htm)
* [Tweening Guide](http://robertpenner.com/easing/penner\_chapter7\_tweening.pdf)
* [Interpolation tricks by Sol](http://sol.gfxile.net/interpolation/#c1)
  * Highly useful for learning about speed graph & math
