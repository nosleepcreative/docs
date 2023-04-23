---
description: Tunnel, zoom, iris - WIP
---

# Radial Array

## Explosion

### Using a normalized range

When using random function for a range, we generally use random(75,400). This works but if we want to upscale the setup, we would need to change both numbers. An alternative is to use a normalize range to multiply a base size eg. random(0.5,1) \* 400 will yield a value between 200, to 400. We can still maintain that ratio even if we change&#x20;

### Base setup&#x20;

$$
random(Radius)*Math.sin(random(theta)+random(force)
$$

```javascript
var seed = thisComp.layer("controls").effect("seed")("Slider");
seedRandom(seed, true);

var mass = random(thisComp.layer("controls").effect("mass")("Slider"));
var a = thisComp.layer("controls").effect("angle")("Slider");
var r = thisComp.layer("controls").effect("radius")("Slider");

r *= random(0.5, 1); // randomize radius
r += (random(.5, 1) * mass); // add random force
var myAngle = random(360);

var theta = degreesToRadians(myAngle);
var x = r * Math.cos(theta);
var y = r * Math.sin(theta);

[x, y] + [thisComp.width, thisComp.height] / 2
```

