---
description: delayed sequential offset - WIP
---

# Staggering

## Abstract

Staggering animation is one of the most common technique used in Motion Design. It's good to know this technique because you need not manually copy and paste keyframes from one layer to another and offset the timing. Instead you can animate one element, and make all the other layers reference that animation with an offset timing.

### Cited sources:

[Creating Trails](http://www.motionscript.com/mastering-expressions/follow-the-leader.html), MotionScript, Dan Ebberts

## Referencing layer index & valueAtTime

Generally, when we want to stagger or offset animations in time for a series of layers, we can make use of the layers' `index` number and the `valueAtTime` property.

#### Basic setup

![](../../.gitbook/assets/staggerAnimation.gif)

```javascript
// Copying animation of a layer, and start it at inPoint of layer
thisComp.layer(index+1).transform.position.valueAtTime(time-inPoint)

// Using delay
offset = 1;
thisComp.layer(index+1).transform.position.valueAtTime(time-offset)    
```

#### Referencing index animated layer

{% tabs %}
{% tab title="1" %}
```javascript
tgt = thisComp.layer("main").transform.position // target layer & prop
delay = 5; //number of frames to delay
delay*= thisComp.frameDuration*(index - 1); // convert to time

tgt.valueAtTime(time - delay)
```
{% endtab %}

{% tab title="2" %}
```javascript
// alternatively you can do it this instead

delay = framesToTime(5); //convert to time method 2
thisComp.layer(1).position.valueAtTime(time - delay)

```
{% endtab %}
{% endtabs %}

#### Cascading index referencing

```javascript
delay = 5; //number of frames to delay

d = delay*thisComp.frameDuration;
thisComp.layer(index - 1).position.valueAtTime(time - d)
```

#### Absolute index referencing&#x20;

It is always best practice to use absolute index referencing, because you do not run the risk of your animation being affected if I were to add a new layer to the composition causing all the layers' index number. The simple way to absolute reference is to:

1. Create a **Null** layer or use your **main** **animated layer**, usually named "start"
2. Make sure the layers you want to offset is **underneath this "start" layer**
3. Get the **absolute index numbe**r by subtracting the Start layer index from the layer index number
4. Now you can use that value to **calculate the delay offset**

```javascript
var startLayer = thisComp.layer("startLayer");
var myIndex = index- startLayer.index;

delay = 5; //number of frames to delay

d = delay*thisComp.frameDuration*(myIndex - 1);
thisComp.layer(1).position.valueAtTime(time - d)
```



#### Scripts

### Adding auto-orientation

```javascript
strt = 0; //start time of template motion
end = 4.0; //end time of template motion

t = thisComp.layer("template");
offset = (t.effect("offset")("Slider")/100)*(index -1);
travel = linear(t.effect("travel")("Slider")/100,strt,end);
if (travel <= offset){
  vect = t.position.velocityAtTime(0);
}else{
  vect = t.position.velocityAtTime(travel - offset);
}
lookAt(position, position + vect)
```

### Following the Null's Orientation

```javascript
strt = 0; //start time of template motion
end = 4.0; //end time of template motion

t = thisComp.layer("template");
offset = (t.effect("offset")("Slider")/100)*(index -1);
travel = linear(t.effect("travel")("Slider")/100,strt,end);

u = t.toWorldVec([1,0,0],travel - offset);
v = t.toWorldVec([0,1,0],travel - offset);
w = t.toWorldVec([0,0,1],travel - offset);

sinb = clamp(w[0],-1,1);
b = Math.asin(sinb/thisComp.pixelAspect);
cosb = Math.cos(b);
if (Math.abs(cosb) > .0005){
  c = -Math.atan2(v[0],u[0]);
  a = -Math.atan2(w[1],w[2]);
}else{
  a = Math.atan2(u[1],v[1]);
  c = 0;
}
[radiansToDegrees(a),radiansToDegrees(b),radiansToDegrees(c)]
```

#### Case studies

{% embed url="https://youtu.be/cLr1YDdqVxg" %}

{% embed url="https://youtu.be/TwbDN8SX058" %}

## Distance-based

### Omni-directional

{% embed url="https://youtu.be/N2E29KvQXgI" %}

```javascript
tgt = thisComp.layer("control");
// d = length(L.transform.position, transform.position);
d = length(thisLayer.toWorld(transform.anchorPoint), tgt.toWorld(tgt.transform.anchorPoint));

delay = thisComp.layer("control").effect("maxDelay")("Slider");
offset = linear(d,0,2000,0,delay);
time-offset;
```

### Radial scale up staggering

![](../../.gitbook/assets/elig\_radial\_scale.gif)

{% tabs %}
{% tab title="nsc" %}
```javascript
// VARIABLES + SETUP
target = thisComp.layer("master").transform.scale; 
maxDist = 1000;
maxDelay = 1;

dst = length(transform.position,[thisComp.width/2,thisComp.height/2]);
delay = linear(dst,0,maxDist,0,maxDelay);

// EXECUTION
target.valueAtTime(time-delay)
```
{% endtab %}

{% tab title="OF" %}
```javascript
//apply to scale
target = thisComp.layer("fade");
fade = target.effect("scale")(1);
delay = target.effect("delay")(1)*thisComp.frameDuration;
dist = length(thisLayer.toWorld(thisLayer.anchorPoint), target.toWorld(target.anchorPoint));
seed = seedRandom(15, true)
randomRange = target.effect("random")("Slider");
rand = (random(-randomRange, randomRange))*thisComp.frameDuration;
offset = delay/dist;
s = fade.valueAtTime(time - offset - rand);
[s,s]
```
{% endtab %}
{% endtabs %}

### Effector opacity fade on

![](../../.gitbook/assets/valueAtTime\_HexTile\_Effector\_Opacity\_demo.gif)

{% tabs %}
{% tab title="nsc" %}
```javascript
//Create a null named "EFFECTOR" 
//Add 2 Slider Control Effects renamed to "maxDist" and "delay"


// EXECUTE
target = thisComp.layer("EFFECTOR").transform
maxDist = thisComp.layer("EFFECTOR").effect("maxDist")("Slider");
maxDelay = thisComp.layer("EFFECTOR").effect("delay")("Slider");

dst = length(transform.position, target.position);
delay = linear(dst, 0, maxDist, 0, maxDelay);

// EXECUTION
target.opacity.valueAtTime(time - delay)
```
{% endtab %}
{% endtabs %}

### Double directional

This allow you to row by row staggering by separating the dimensions for measuring distances.

```javascript
//user variables 
tgt = thisComp.layer("control");
delayX = 1;
delayY = 2;
distanceX = 1920;
distanceY = 400;

// logic
d1 = length(tgt.toWorld(tgt.transform.anchorPoint)[0],transform.position[0])
d2 = length(tgt.toWorld(tgt.transform.anchorPoint)[1],transform.position[1])
offsetx = linear(d1,0,distanceX,0,delayX);
offsety = linear(d2,0,distanceY,0,delayY);

//main
time-offsetx-offsety
```
