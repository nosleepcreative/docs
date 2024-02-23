# Rendering & Lighting

## **Using flipbook**

Good for fast preview animation

* Exporting as avi  = large file > compressed via Handbrake
* MPlay, export > ffmpeg > as mp4

## IPR render

## Orange lighting exercise&#x20;

* Noise bumps- In Principled Shader > Displacement > Noise Displacement
* PBR renders
* environment light
  * unlink sunlight
  * change to Area, normalize, back to sun
  * change sun angle
* Shadow noise
  * increase min/max ray samples to 16/32
* Importance of EXR

## **Notes**

* Using separate mantra nodes for test and finder render
* force object & exclude object
* tiled renders, and restitching them&#x20;

## Using img network

* nodes: bright, over, color
* resizing flat background

Lights

point lights - good for bulb

disk light highlights

Mantra

mind your samples

reflect limit 10 - 15 (glass), turn down if not reflecting

DOF in Compositing, not in render

Motion Blur in renderer

Using commandline rendering script - rename version, mantranode, and hip file

**Optimizing render times**

Tiled render - Quick render by reducing tile to 2, and specify tile index



## 🔦 Lighting

| Lights                                 |   |
| -------------------------------------- | - |
| <p>sunlight &#x26; keylight</p><p></p> |   |
|                                        |   |

distant - cheaper, good for blocking

sun - blurred shadow

Spotlight - not so good

attenuation, active radius - good for instancing lights

Light bank

Data tree

Mantra > Objects > Headlight Creation

Simulating warm and cool lights to create dimensions

Lighting linking - for more controls

**Instancing lights**

instancing - pack geometry - does not inherit all details

`attribcreate`

you cannot see instances till you render it
