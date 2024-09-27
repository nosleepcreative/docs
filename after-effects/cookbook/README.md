# Cookbook

{% hint style="danger" %}
Encoutering expression errors? Check out this [Troubleshooting Guide!](https://app.gitbook.com/o/NW5KuSR8Tekqe0Wvv3JX/s/-Lgx0HTP5iKvQQwXUStq/\~/changes/1080/after-effects/expressions/expression-troubleshooting)
{% endhint %}

## Introduction

Below are code used in my [YouTube tutorials](https://www.youtube.com/@NoSleepCreative/videos) for your reference and usage. This page&#x20;

## Phyllotaxis

{% embed url="https://www.youtube.com/watch?v=K1P9NgVJqLQ" %}

```javascript
//theta
var myIndex = index - thisComp.layer("controls").index;
var a = 137.508
var theta = degreesToRadians(myIndex * a);

theta

//position
var myIndex = index - thisComp.layer("controls").index;
var s = thisComp.layer("controls").effect("Spacing")("Slider");
var theta = effect("theta")("Slider");

x = s * Math.sqrt(myIndex) * Math.cos(theta);
y = s * Math.sqrt(myIndex) * Math.sin(theta);

[x, y] + [thisComp.width, thisComp.height] / 2

// Circle Size
var theta = effect("theta")("Slider");
var minSize = thisComp.layer("controls").effect("Min Size")("Slider");
var maxSize = thisComp.layer("controls").effect("Max Size")("Slider");
var maxRange = thisComp.layer("controls").effect("Distance Range")("Slider");

var sizeFactor = linear(theta, 0, maxRange, minSize, maxSize) / 100;
var s = thisComp.layer("controls").effect("Size")("Slider");
[s, s] * sizeFactor;

// Fill Color
var theta = effect("theta")("Slider");
var interval = thisComp.layer("controls").effect("Color Interval")("Slider");
var numColor = thisComp.layer("colors")("Effects").numProperties;

var colorIndex = Math.ceil(theta / interval) % numColor + 1;
thisComp.layer("colors").effect(colorIndex)("Color")


```

## Best Motion Trails in After Effects

{% embed url="https://www.youtube.com/watch?v=9MCHTe8iBpk" %}

### Wavey sine wave motion&#x20;

```javascript
// apply to X position after separating dimensions
var vel = effect("waveSpeed")("Slider")*Math.PI*2;
var amp = effect("waveHeight")("Slider");
var offset =Math.PI*2*degreesToRadians(effect("phase")("Angle"));

// main 
var v = amp* Math.sin(time*vel+offset);
v + value;
```

### createPath Motion Trails

```javascript
//setup 
var l = effect("Layer Control")("Layer");
var dur = effect("trailLength")("Slider");
var pts = [];

// calculate the trail length in frame numbers 
var currentFrame = timeToFrames(time);
var trailLength = currentFrame - dur;

// main: generate the points from the current time 

for (i = currentFrame; i > trailLength; i--) {
    t = framesToTime(i)
    ap = l.toWorld(l.transform.anchorPoint, t);
    ap -= [thisComp.width, thisComp.height] / 2;
    pts.push(ap);
}

// create the path using the points
createPath(pts, [], [], 0)
```

## Scaling Radial Grid

{% embed url="https://www.youtube.com/watch?v=8BeI1qXzysU" %}

### Parent/Child Link without scale inheritance

```javascript
ps = parent.transform.scale.value;
s = value[0]*100/ps[0];
[s,s]
```

### Aim Constraint

```javascript
target = thisComp.layer("controls"); // set this to the layer to aim at
p = thisLayer.toWorld(anchorPoint) - target.position;
radiansToDegrees(Math.atan2(p[1], p[0])) - 90
```

## Cyberpunk tech lines

{% embed url="https://www.youtube.com/watch?v=Gfr0sUY5eo0&t" %}

{% tabs %}
{% tab title="main" %}
```javascript
// user variables 
var pts = 50;
var pos = [0, 100];
var seed = 50;

// declaration 
var x, y; // coordinates
var c, mul; // direction changer
var vertices = [[0, 0]]; // create first point 

// vertices array 
for (i = 1; i <= pts; i++) {
  seedRandom(i + seed, true);
  c = random(); // create random num between 0 to 1 
  c > 0.5 ? mul = 1 : mul = -1; // change direction 
  oldEle = vertices[i - 1]; // get previous vertice

  y = random(pos[0], pos[1]);
  x = y * mul;

  // conditional: if even, go diagonal. If odd, go straight
  if (i % 2 == 0) {
    vertices[i] = oldEle + [x, y];
  } else {
    vertices[i] = oldEle + [0, y];
  }
}

createPath(vertices, [], [], 0);
```
{% endtab %}

{% tab title="branch" %}
```javascript
// user variables 
var pts = effect("pts")("Slider");
var pos = [effect("min_y")("Slider"), effect("max_y")("Slider")];
var seed = effect("seed")("Slider");

// get random point on first path
seedRandom(seed,true);
var myPath = content("main").path;
var myPathpts = myPath.points().length;
var myRandPt = Math.floor(random(myPathpts));
var mySelectedPt = myPath.points()[myRandPt];

// declaration 
var x, y // coordinates
var c, mul // direction changer
var vertices = [mySelectedPt] // create first point 

// vertices array 
for (i = 1; i <= pts; i++) {
  seedRandom(i + seed, true);
  c = random(); // create random num between 0 to 1 
  c > 0.5 ? mul = 1 : mul = -1; // change direction 
  oldEle = vertices[i - 1] // get previous vertice

  y = random(pos[0], pos[1]);
  x = y * mul;

  // conditional: if even, go diagonal. If odd, go straight
  if (i % 2 == 0) {
    vertices[i] = oldEle + [x, y];
  } else {
    vertices[i] = oldEle + [0, y];
  }
}

createPath(vertices, [], [], 0);
```
{% endtab %}
{% endtabs %}

## Radial Delay Rig

{% embed url="https://youtu.be/N2E29KvQXgI" %}

```javascript
tgt = thisComp.layer("control");
// d = length(L.transform.position, transform.position);
d = length(thisLayer.toWorld(transform.anchorPoint), tgt.toWorld(tgt.transform.anchorPoint));

delay = thisComp.layer("control").effect("maxDelay")("Slider");
offset = linear(d,0,2000,0,delay);
time-offset;
```

## Buck Apeel Circle Ripple

{% embed url="https://www.youtube.com/watch?v=TwbDN8SX058&feature=youtu.be" %}

**Ensure you have the following**

1. ring shape layer `Slider Controls` : size,copies, radius (anchorpoint-Y), myIndex
2. null layer named "controls" with `Slider Controls` : circle\_size, circle\_spacing, ring\_base\_size, ring\_spacing, dur
3. null layer named "colors" with `Color Controls` x 3

### **Auto-copies**

```javascript
cir = 2*Math.PI *effect("radius")("Slider"); // circumference of circle
n = thisComp.layer("controls").effect("circle_spacing")("Slider"); // max size of a circle
Math.floor(cir/n) // round down the results
```

### **Get myIndex**

```javascript
myIndex = index-thisComp.layer("controls").index-1;
```

### **Auto-scaling radius**

```javascript
myIndex = effect("myIndex")("Slider"); 
c = thisComp.layer("controls");
int = c.effect("ring_spacing")("Slider");
base = c.effect("ring_base_size")("Slider");

s = myIndex*int;s+ base;
```

### Auto-alternate color

```javascript
myIndex = effect("myIndex")("Slider"); 
num = myIndex %3+1;
thisComp.layer("color").effect(num)("Color")
```

### Stagger-animation - balls

```javascript
myIndex = effect("myIndex")("Slider"); 
s = thisComp.layer("controls").effect("circle_size")("Slider");
dur = framesToTime(thisComp.layer("controls").effect("dur")("Slider"));
offset = myIndex*dur;
s.valueAtTime(time-offset)
```

## Matrix Binary Rain Code

{% embed url="https://youtu.be/p2r_abV9HL8" %}

```javascript
seed = 10; // connect to slider
n = 50; // connect to slider

m = b = ''

for(i=0;i<n;i++){
	seedRandom(seed+i,true);
	b = Math.round(random());
	m += b;
}
```

## Vucko — _From Nothing to Something_

{% embed url="https://youtu.be/1wrFAGKLGDk" %}

### Random flickering&#x20;

```javascript
// apply this to your Time Remap property of your Sprite render 
seed = 20; // option:connect to a slider 
segMin = .5; //minimum segment duration
segMax = .8; //maximum segment duration
flickerDurMin = 1;
flickerDurMax = 5;

end = 0;
j = 0;

while ( time >= end){
  j += 1;
  seedRandom(j,true);
  start = end;
  end += random(segMin,segMax);
}
flickerDur = random(flickerDurMin,flickerDurMax);
if (time > end - flickerDur){
  seedRandom(j+69+seed,true);
  random(outPoint);
}else{
   seedRandom(j+seed,true);
  random(outPoint);
}

// original expression from Dan EbbertyVelocity = 200; //pixels per second
```

## Change Log

* 2021: Initial publish
* 2024.09.27: Added introduction, moved troubleshooting guide to a separate page
