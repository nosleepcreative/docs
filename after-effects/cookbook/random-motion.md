---
description: WIP - last updated 21 April 2021
---

# Random properties

## Abstract

{% embed url="https://youtu.be/nqf5n_y7mE8" %}

One of the most useful things you can do with Expressions is **randomizing layer properties.** Some properties include transform properties (position, rotation, scale, or opacity), color, or even Time Remap. **Learning to randomize properties is a good beginner exercise to raise one's comprehension of Javascript Expression. In this page, we will cover different ways to randomize properties.**

### **Understanding Random functions**

* random()
* random(minValue, maxValue)
* seedRandom(seed, timeless=false)

Core skills: randomize values, arrays, color

{% hint style="info" %}
**What is a seed?**\
\
A random seed (or seed state, or just seed) is a number (or vector) used to initialize a pseudorandom number generator. **To put simply, different seed number yield difference sequence of random number.**
{% endhint %}

## Position

### Wiggle

```javascript
wiggle(20,50);

// wiggle x axis 
x = wiggle(20,50)[0];
y = value[1];
pos = [x,y]

// wiggle y axis 
x = value[0[;
y = wiggle(20,50);
pos = [x,y]

// getting wiggle increment values only 
inc = wiggle(20,50)-50;
```

{% embed url="https://youtu.be/a5JIRHATV4I" %}

### positioning&#x20;

```javascript
// randomize between a range 
seedRandom(1,true);
x = random(300,1920);
y = random(500,1080);
[x,y];
```

```javascript
// using arrays and variable 
seed = 20;
min = [25,25,-1900]; 
max = [thisComp.width,thisComp.height,50]

seedRandom(seed,true);
random(min,max);

/* This is same as this
x= random(min[0],max[0]);
y= random(min[1],max[1]);
z= random(min[2],max[2]);
[x,y,z];
*/
```

## Opacity

### Flickering / Strobe

![](../../.gitbook/assets/flicker\_Ebbert.gif)

```javascript
// VARIABLES
    minSeg = 1.5; //minimum interval (must be > 0) 
    maxSeg = 2.5; //maximum interval (must be > minSeg) 
    
    // flickering duration
    minFlicker = .5; //must be less than minSeg 
    maxFlicker = 1; // must be less than minSeg 
    flickerDur = random(minFlicker,maxFlicker);
    
    //initial conditions
    segEndTime = 0; 
    i = 1; 

// Continuous loop: create a fixed random segment value and add to segEndTime
while (time >= segEndTime){ 
    i += 1; 
    seedRandom(i,true); 
    segEndTime = segEndTime + random(minSeg,maxSeg); 
} 

// Switch back to use the current time as input to the random seed.
seedRandom(1,false); 

// As time > threshold, flicker
if (time > segEndTime - flickerDur){random(0,100) }else{ 100 }

// Source: http://www.motionscript.com/expressions-lab-ae65/swinging-light.html
// Also see: http://www.motionscript.com/mastering-expressions/random-3.html
```

### Wiggle&#x20;

![](../../.gitbook/assets/randomFade.gif)

```javascript
// control = thisComp.layer("control"); // connect to null layer with sliders
freq = 1;
amp = 100;
octave = 1;
amp_mult = 3;

wiggle(freq, amp, octave, amp_mult, time)
```

### Wiggle with flicker&#x20;

![](../../.gitbook/assets/randomFade\_withFlicker.gif)

```javascript
// control = thisComp.layer("control"); // connect to null layer with sliders
freq = 1;
amp = 100;
octave = 1;
amp_mult = 3;

opacity = wiggle(freq, amp, octave, amp_mult, time)


// VARIABLES
minSeg = control.effect("minSeg")("Slider"); //minimum interval (must be > 0) 
maxSeg = control.effect("maxSeg")("Slider");; //maximum interval (must be > minSeg) 

// flickering duration
minFlicker = control.effect("minFlicker")("Slider");; //must be less than minSeg 
maxFlicker = control.effect("maxFlicker")("Slider");; // must be less than minSeg 
flickerDur = random(minFlicker, maxFlicker);

//initial conditions 
segStartTime = 0;
segEndTime = 0;
i = 1;

// Continuous loop: create a fixed random segment value and add to segEndTime
while (time >= segEndTime) {
    i += 1;
    seedRandom(i, true);
    segStartTime = segEndTime;
    segEndTime = segEndTime + random(minSeg, maxSeg);
}

// Switch back to use the current time as input to the random seed.
seedRandom(1, false);

// As time moves threshold, flicker
if (time > segEndTime - flickerDur) {
    random(0, 100)
} else {
    opacity
}
```

### Using sine function

![](../../.gitbook/assets/flicker\_rand\_sin.gif)

```javascript
// Mass flickering
vel = 50;
seedRandom(0,true);
Math.sin(time*vel+random(index))*100;
```

![](../../.gitbook/assets/flicker\_rand\_sinIndex.gif)

```javascript
// 'Wave flickering'
vel = 50;
seedRandom(0,true);
Math.sin(time*vel+index)*100;

// Combining 
bool = 1;
vel = 50;
seedRandom(0,true);
wave=Math.sin(time*vel+index)*100;
rand =Math.sin(time*vel+random(index))*100;
bool==0 ? wave : rand;
```

### Random pop on

![](../../.gitbook/assets/random\_opacity\_turnon.gif)

```javascript
seed = 29;
threshold = linear(time,0,thisComp.duration,0,100); // or Connect to slider to animate switch on & off

seedRandom(seed,true);
randValue = random(0,90);

if(randValue < threshold){
    100;} else 0
```

Tutorial: [Randomly Reveal Layers & Emojis with Expressions](https://www.youtube.com/watch?v=8MAo1T2rNK4), NSC&#x20;

### Random fade on&#x20;

![](../../.gitbook/assets/rand\_opacity\_fadeon.gif)

{% tabs %}
{% tab title="v2" %}
```javascript
var seed = 1;
var seedRandom(seed,true);

var startTime = 0; // specify when fade starts
var delay = random(0,1); // random delay
var fadeDur = framesToTime(20); // duration of fade

linear(time, startTime + delay, startTime + delay + fadeDur, 0, 100)
```
{% endtab %}

{% tab title="v1" %}
```javascript
seed = 1;
seedRandom(seed,true);
startTime = random(0,1); // random start time
dur = framesToTime(20); // duration of fade

linear(time, startTime, startTime + dur, 0, 100)
```
{% endtab %}
{% endtabs %}

## Random Color

### RGB color

```javascript
// Apply on a color property eg. Fill, Shape Fill
seedRandom(1,true);
random([0,0,0,1],[1,1,1,1])
```

### **From a color palette**&#x20;

{% embed url="https://youtu.be/1wrFAGKLGDk" %}

### Sequential cycling color from a palette

```javascript
// user variables
var vel = 2 ;
var numCol = 5;

//main
var inc = Math.floor(time * vel) + index; // counter
var n = inc % numCol + 1; // keep the num between 1 & numCol value

// reference a null with colors controls only 
thisComp.layer("controls").effect(n)("Color"); 
```

1. retrieve the absolute index of a layer,
2. add a slider that increment by a value at a set interval
3. do the mod calculation

### Random cycling color from a palette

```javascript
// user variables
var mySpeed = posterizeTime(3);
var colorNull = thisComp.layer("controls"); 

// calculate num of color controls
var numFx = colorNull("ADBE Effect Parade").numProperties;
var numCol = 0;
for (i = 1; i <= numFx; i++) {
    if (colorNull.effect(i).name.includes("Color")) {
        numCol += 1;
    }
}

// main
var n = Math.ceil(random(numCol));
thisComp.layer("controls").effect(n)("Color");
```

#### Get num of color controls

{% tabs %}
{% tab title="includes" %}
```javascript
var colorNull = thisLayer("ADBE Effect Parade");
var numFx = colorNull.numProperties;
var numCol = 0;
for (i = 1; i <= numFx; i++) {
    if (thisLayer.effect(i).includes("Color")) {
        numCol += 1;
    }
}
numCol;
```
{% endtab %}

{% tab title="search" %}
```javascript
var numFx = thisLayer("ADBE Effect Parade").numProperties;
var numCol = 0;
for (i = 1; i <= numFx; i++) {
    if (thisLayer.effect(i).name.search("Color") >= 0) {
        numCol += 1;
    }
}
numCol;
```
{% endtab %}
{% endtabs %}

## Time Remapping / Playback

![](../../.gitbook/assets/EXP\_Counter.gif)

### Random frame playback

```javascript
// Source Dan Ebbert

fr = 12; // frame rate;

numFrames = 8;

seedRandom(index,true);

seg = Math.floor(time*fr);

f = Math.floor(random(numFrames));

for (i = 0; i < seg; i++)

  f = (f + Math.floor(random(1,numFrames)))%numFrames;

framesToTime(f);
```

### Random delayed/advanced layer playback

```javascript
var seed = 1;
var seedRandom(seed,true);
var myDelay = random(1,10);
var time - myDelay;
```

### Play one frame at a time (without 'float time')

```javascript
var fps = 1;
x = framesToTime(Math.round(time*fps))
//There probably is a better way but I cannot figured it out right now.
```

### Random still frame (Good for spriting)

```javascript
//Apply this to a composition with a image sequence inside
seedRandom(0,true);
t= random(0,72);
framesToTime(t);
```

* for spriting images,
* refer to CoMotion 2021 title sequence background&#x20;

## Source text & strings

### [Generating non-repeating random numbers](https://www.codegrepper.com/code-examples/javascript/generating+non+repeating+random+nubmers+in+js)

```javascript
var nums = [1,2,3,4,5,6,7,8,9,10],//all numbers to be randomized
    ranNums = [],
    i = nums.length,
    j = 0;

while (i--) {
    j = Math.floor(Math.random() * (i+1));
    ranNums.push(nums[j]);
    nums.splice(j,1);
}
ranNums
```

### Using text animators

### Binary

{% embed url="https://youtu.be/p2r_abV9HL8" %}

### From a specific set of characters or words

eg. Matrix katakana

## Building a Randomizing rig or preset

Core skills: randomize time, Spriting, building controls, conditional randomizing with modulo operator (alternate colors)

{% hint style="info" %}
Keep in **After Effects scripting,** the random function only returns a random number between 0 to 1. What this means is that you cannot do  use **`random(20,30)`** to generate a random value between 20 and 30. You have to write a function for that, which you can reference [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Math/random).
{% endhint %}

## Randomizing with AE scripts

1. Download Jeff Almasol's script from aescript or redefinery
2. Install script via After Effects or putting directly into the Applications folder
3. Modify values
4. Select layers, and run script file&#x20;
