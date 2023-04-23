# cookbook

## Spline wrapping&#x20;

### Using animated textures&#x20;

### **Faux cel smoke & stroke**

In order to cut down the time and effort on cel animation, I experimented with using Spline Wrap and anmated texture in C4D to create a faux cel animation.

Pros

* Tapering can be done in C4D `spline wrap` deformer instead of doing in AE

#### Preparing of animated texture

* In AE,
  * baseline of sprite footage should in the middle of the composition
* In C4D
  * Luminance: add footage as texture
  * Alpha: uncheck soft & invert, check image alpha & pre-multiplied
  * plain geometry behind smoke to hide white of textures
  * `anti-aliasing` [set to best](https://www.youtube.com/watch?v=BurycwERSts)

#### Troubleshooting

* Having the spline wrap disappear once the animation is done; I made use of a simple Python conditional
* Manually change the start time of the animation texture
* Setting textures using Xpresso causes rendering to be completely black

## Randomizing Colors&#x20;

### With Mograph Material

{% embed url="https://www.youtube.com/watch?v=rXQyO_QLwH0" %}

{% embed url="https://www.youtube.com/watch?v=TXl1a0fmzT8" %}

