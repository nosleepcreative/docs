# Rendering

## Mantra

* **Camera**
*
  * Change resolution, camera properties
* Light
  * Color Editor: create complementary colors
* Render Settings
* **Data tree > Light Bank**
  * rename all lights and change their properties
* Out > **Mantra node**
  * Resolution Scale&#x20;
  * padding: $F4.jpg > 0001.jpg
  *
  * **Images tab**
    * Extra Image planes (AOV)
      * Image passes
  * **Rendering tab**&#x20;
    * Rendering engine: PBR
    * Pixel sample: increase to reduce noisy renders
    * Limits
  * **Objects tab**
    * **Candidate objects: \* (all)**
      * Using bundles - @bundleName

## Settings

* Pixel samples — antialiasing (higher values = less noise)
* Samplings — noise levels
  * Min Ray samples
  * Max Ray samples

## Jason iversen PBR

* Pixel Samples: 7x7 (up to 10x10 if the scene really needed it)
* Min/Max Ray Samples: 1/9 – sometimes 2/9
* Noise Level: 0.08 (this seemed good enough to us … less than film grain)
* Reflect/Diffuse Limits: 2, 2
* Color Space: Gamma 2.2
* Color Limit: 4 (your 1 is clamping way too hard)
* Photons: 2m photons for a huge room. Yours is 7m! I'm sure 1m is fine for this space. Ratio was 2.5.

Source: [https://www.sidefx.com/forum/topic/21548/](https://www.sidefx.com/forum/topic/21548/)
