---
description: Written on Mar 10, 2021. Last updated on ... — WIP
---

# Harmonic Motion

## Abstract

Harmonic oscillations or sine waves are commonly observed in the trends of Motion Design (as of 2021). It seems Mathematics or Trigonometry plays a significant role in art and design. This page will served to inform Motion Designers how the Math behind sine wave works and how you can use it in animation, or use to generate waves paths or shapes

#### Why does it matter?

For those who are allergic or have distaste for Mathematics or Trigonometry, I like you to refresh your understandings of how we can use these concepts to:&#x20;

1. **Make complex animations** that may be impossible or tedious to do manually
2. **See animation in terms of data and numbers.** When I see animations like this, I do not see keyframes, but rather a sine wave being modulated to create a wavy motion \[insert animation ref].

#### **Readings**

* [https://www.motionscript.com/mastering-expressions/simulation-basics-1.html](https://www.motionscript.com/mastering-expressions/simulation-basics-1.html)
* [Math.sin](https://www.youtube.com/watch?v=Oiiq4wmbuPo\&t=160s), Evan Abrams
* [JS Math](https://www.w3schools.com/js/js\_math.asp), w3schools
* [Periodic functions](https://www.mathsisfun.com/algebra/amplitude-period-frequency-phase-shift.html), mathsisfun
* [Harmonic](http://www.jjgifford.com/expressions/geometry/harmonic.html), jjgifford

#### Text

1. Ordinary Folk
2. iLLo,
3. Flatwhite Motion
4. Gunner

## Oscillations

### Terminology

* **Crest** — maximum value of upward displacement within a cycle
* **Trough** — minimum or lowest point in a cycle.
* **Cycle** — An oscillation, or cycle, is defined as a single change from up to down to up, or as a change from positive, to negative to positive.\

* **Wave Length:** the distance between two successive crests (period)or troughs of a wave.
* **Wave Height:** the vertical distance between the trough of a wave and the following crest\

* **Amplitude —** the height from the center line to the peak (or to the trough). Or we can measure the height from highest to lowest points and divide that by 2.&#x20;
* **Frequency —** the number of occurrences of a repeating event per unit of times\

* **Phase** —the location or timing of a point within a wave cycle of a repetitive waveform.
* **Phase shift** —  how far the function is shifted horizontally from the usual position.
* **Radian** — a unit of measure for angles that is based on the radius of a circle. A circle has 360° or 2pi radians.&#x20;

### Sine wave

$$
A*Math.sin(\theta + C)
$$

* **amplitude** is A
* **phase** is theta
* **phase** **shift** is C



{% hint style="info" %}
**Why do we do append "Math." before sin?**&#x20;

This is because when we are writing expressions, we are using the **Javascript language of a Math object** to perform mathematical tasks on numbers. Some examples you may have seen include Math.cos, Math.round, or Math.ceil . You can learn more about it at [w3schools](https://www.w3schools.com/js/js\_math.asp).
{% endhint %}

### Cosine wave

## Practical applications

### Creating sine wave loops with varying frequency

* If you are creating a looping animation with a series of sine wave with varying frequencies, you have to determine the duration of the composition, or vice versa.
* If your waves include frequencies of 1, .5, .2. Your composition duration should be 5s or multiple of 5s, because the slowest frequency is .2. For that wave to finish one cycle, it takes 1 second / 0.2 = 5 seconds.
* Hence, it's a game of multiplication and time tables. For more complex variations such as frequency values of 0.3, 0.4, 0.5, you will have to find a common denominator (.333,2.5,2) = 10s .

## Why generate paths with expressions

* My main concerns is aliasing issues, by using shape layers, we avoid jagged edges that are present when you use wave warp effect with a high wave height.&#x20;

## Amplitude modulation

### Frequency increasing

## Fractions & for-loop in createPath

In order to generate a smooth wavy line, we have to generate many points sticking close together to maintain curvature. This is because we do not want to be concerned with writing a function to calculate the in and out tangents.

## Damped Sine Wave

![](../../.gitbook/assets/createPath\_damped\_sine.gif)

Source: [_An Ordinary Christmas_ work files](https://www.ordinaryfolk.co/play), Ordinary Folk

```javascript
S = effect("Speed")("Slider");
A = effect("Amp")("Slider"); 
F = effect("Freq")("Slider") / 3.6;
R = effect("Resolution")("Slider");
W = effect("Width")("Slider");
E = effect("Exp")("Slider") * 100;

P = [];

for (i = 0; i < R; i++) {
    x = W / R * i * Math.exp(i / E)
    y = i * Math.exp(i / E) * Math.sin((time - inPoint) * S + i / (R / F)) * A;
    P.push([x, y]);
}

createPath(P, [], [], false)
```
