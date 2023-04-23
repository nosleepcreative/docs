---
description: Posted 2021, Updated on 10 Apr 2021
---

# Cookbook

## 🔴 Why is my expression not working?

{% hint style="danger" %}
Biggest culprit: You are using **ExtendScript for the Expression Engine,** when it is supposed to be Javascript.\
\
**Fix:** Go to File> Project Settings > Expressions > change to Javascript. ([This option is available on AE 2019 and later.](https://help.pixflow.net/portal/en/kb/articles/after-effect-change-expression-engin))&#x20;
{% endhint %}

#### Other reasons

1. You made a **typo or used the wrong case** when writing the variable or function names
2. You listed a **single value** into a parameters that takes an **array**&#x20;
   * eg. myScale =5  will yield an error because the scale property is an array that takes 2 values.
   * The fix is&#x20;
     * myScale = \[5,5];&#x20;
     * or myScale = 5; s = \[myScale, myScale]
3. You forgot to put **semicolons** at the end of each line
4. **You listed a variable as a string value**&#x20;
   * This is a string: "mytext"
   * This is a variable: var str  = "mytext";
   * eg. in Apeel & Vucko tutorial, people alway list the variable as a string (**'myVariable'**) when it should be just **myVariable**;

**When to ask for help?**

If you tried everything above, and nothing still works. There are two things you can do:

1. You can **download the project files** that I usually provide for free, and use my code I have there. As I am just a student, and do this on my own freewill. I do not have a lot of time and bandwidth to help people troubleshoot expressions. Hence, it's up to you to figure it on your own as much as possible.
2. **If you have to ask me for help,** what I appreciate is having **more context and description** of your problem. For example:

* Which lines does the error occurred?
* What does the error(s) say?
* What have you tried?&#x20;
* Have you consulted this guide and tried the solutions I mentioned?
* What AE version are you running, and what OS.

**Sample format for requesting troubleshooting**

_Hello, I having `problem` with `line number`. The error says `errorMessage` . I have tried `solution` but I still cannot fix the issue._&#x20;

**What does not help me**

1. Saying that "I wrote the code exactly" or I followed your tutorial. If you did, it would have worked. Clearly, the issue is something else and usually it's simply just a typo mistake.Hence, please give me more information about what the problem is so I can help you as quickly as possible.

#### More readings

* [How to troubleshoot expressions errors](https://www.youtube.com/watch?v=VdaGqq4I0qM\&t=1426s), Intro to Expression Rigs in After Effects, Zack Lovatt

## Phyllotaxis

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

// original expression from Dan Ebbert
```

## Falling leaves \[[1](https://www.aenhancers.com/viewtopic.php?t=8)]\[[2](https://aenhancers.com/viewtopic.php?t=655)]

{% tabs %}
{% tab title="1" %}
```javascript
//position
yVelocity = 200; //pixels per second
oscFreq = 1.5; //oscillations per second
oscDepth = 35; //oscillation depth (pixels)
drift = 25; // drift (wind?) (pixels per second: - = left, + = right)

value + [oscDepth*Math.sin(oscFreq*Math.PI*2*time) + drift *time, yVelocity*time,0]

//Z ROTATION:

seedRandom(index,true);
random(360);

//Y ROTATION:
oscFreq = 1.5;
maxTilt = 15; //degrees

maxTilt*Math.cos(oscFreq*Math.PI*2*time)
```
{% endtab %}

{% tab title="2" %}
```
yVelocity = 200; //pixels per second
oscFreq = 1.5; //oscillations per second
oscDepth = 35; //oscillation depth (pixels)
drift = 25; // drift (wind?) (pixels per second: - = left, + = right)
floor=500; //position of floor from top

X=value[0] + oscDepth*Math.sin(oscFreq*Math.PI*2*time) + drift *time;
Y=easeIn(value[1]+yVelocity*time,value[1],floor)
Z=0;

[X,Y,Z]
```
{% endtab %}
{% endtabs %}

## Techniques

### Radial arrangement

* [**place along path** ](https://www.youtube.com/watch?v=wmbIebDsWn0)&#x20;

### Pixilation

* **Dot-Pixilation:** CC Ball Actions
* **Square-Pixilation:** Mosaic
* Plugins: tv pixels,

### Multi-image spriting / instancing

```javascript
// Create a marker and use that to control the length of the comp you want instance

seedRandom(0,true);
m = thisComp.marker.nearestKey(time).time
random(0, m)
```

​
