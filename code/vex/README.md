# Houdini

## Recommended Readings

#### Industry / Case Studies

* ​Rohan Dalvi&#x20;
* Entagma

#### Documentation / Tutorials&#x20;

* [**https://www.sidefx.com/docs/houdini/vex/index.html**](https://www.sidefx.com/docs/houdini/vex/index.html)
* [**VEX Language Reference**](https://www.sidefx.com/docs/houdini/vex/lang.html)
* [**VEX Functions**](https://www.sidefx.com/docs/houdini/vex/functions)
* [https://www.sidefx.com/learn/getting\_started/](https://www.sidefx.com/learn/getting\_started/)
* [https://www.hipflask.how/](https://www.hipflask.how/)
* [https://www.sidefx.com/docs/houdini/](https://www.sidefx.com/docs/houdini/)
* [https://www.sidefx.com/forum/](https://www.sidefx.com/forum/)
* [SideFX Digital Learning Material](https://docs.google.com/spreadsheets/d/11FbYBV\_OV2INv3LCk38fmcgZbuVrgxYaZK-1KifCpyc/edit#gid=0)&#x20;
* Algorithmic
  * [Junchiro Horikawa](https://www.youtube.com/c/JunichiroHorikawa/videos)

**Repositories / Wiki**

* [Deborah Fowler](http://www.deborahrfowler.com/HoudiniResources/HOUDINI-RESOURCES.html)
* [**Tokeru**](http://www.tokeru.com/cgwiki/?title=Houdini)
  * [Joy of VEX](http://www.tokeru.com/cgwiki/index.php?title=JoyOfVex)
* [**Tosin Akinwoye**](https://tosinakinwoye.com/2017/01/23/houdini-vex-snippets/)
* [**Kiryha**](https://github.com/kiryha/Houdini)
* [**Jtomori**](https://github.com/jtomori/vex\_tutorial/blob/master/README.md)
* [**John Kunz**](http://mrkunz.com/blog/08\_22\_2018\_VEX\_Wrangle\_Cheat\_Sheet.html)

**Mathematics**

* Khan Academy
* [Procedural noise](https://www.scratchapixel.com/lessons/procedural-generation-virtual-worlds/perlin-noise-part-2)
* [**3Blue1Brown​**](https://www.youtube.com/channel/UCYO\_jab\_esuFRV4b17AJtAw)
* [Cross Product and Dot Product: Visual explanation](https://www.youtube.com/watch?v=h0NJK4mEIJU)
* [The Applications of Matrices | What I wish my teachers told me way earlier](https://www.youtube.com/watch?v=rowWM-MijXU\&feature=youtu.be)[ers told me way earlier](https://www.youtube.com/watch?v=rowWM-MijXU\&feature=youtu.be)

## **Abstract**

* **Houdini** is a 3D software known for it's procedural generation tools. The word procedural might sound vague to you but in short what it means to to me is that:
  * Non-destructive setup&#x20;
  * Flexibility and adaptability
  * The software do most of the work; you just need to create the tools&#x20;
* This software has a steep learning curve, and it is especially difficult if you have not used a node-based software such Nuke previously. **It is natural not to comprehend what you are doing where you are starting out;** just keep watching tutorials daily and one day your brain will somehow makes sense of the things you never thought you understand. This pretty much applies to learning of any subject matter.
* To get started with Houdini, start by thinking in "points". If you can manipulate points in any way you want; you would have no problem with the software.

## Shortcuts

| Function                           | Windows                  | Mac                                       |
| ---------------------------------- | ------------------------ | ----------------------------------------- |
| <p></p><p>View properties </p>     |                          | MMB                                       |
| Reveal Properties Panel            |                          | P                                         |
| <p>Align nodes<br>Layout nodes</p> |                          | <p>Hold A + Drag (Down/Right)</p><p>L</p> |
| Move in-out of nodes               |                          | U & I                                     |
| Cut node connection                |                          | Y                                         |
| Radial Menu                        |                          | V                                         |
| Network box                        |                          | shift + O                                 |
| Camera views                       |                          | Cmd 1/2/3/4                               |
| Delete Channel                     |                          | Ctrl + Shift + LMB                        |
|                                    |                          | Shift W                                   |
| Save Quickview                     | Ctrl + numpad 6-9        | Cmd + numpad 6-9                          |
| Load Quickview                     | Space+ numpad 6-9        |                                           |
| Go to next / previous level        | Alt + Left / Right arrow |                                           |

## Terminology

| Item   | Description                                                                                                                                                                                                                                                                                                                                        |
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Object | **Object type nodes in an Object type folder.** These Object nodes allow you build transform constraint hierarchies. Geometry type Object nodes contain SOP nodes that construct and modify geometry that inherit any transforms at the object level.                                                                                              |
| SOPs   | **Surface Operators** or geometry nodes that are inside an object folder. These are used to construct and modify geometry. Any kind of geometry from polygons to volumes.                                                                                                                                                                          |
| DOPs   | **Dynamic Operators** or simulation/solver nodes that are used to construct simulations. Simulations read in geometry from SOPs and passes this data in to the DOP solvers.                                                                                                                                                                        |
| SHOP   | **Shading Operator**s are materials that represent a shader to apply to geometry. Some are hard coded with vex and others are folders that you can dive in to and modify the VOPs inside.                                                                                                                                                          |
| VOPs   | **Vector Operators** inside VOP network nodes are used for everything from building shaders to modifying geometry, volumes, pixels, and more.                                                                                                                                                                                                      |
| VEX    | **Vector Expression Language.** The code language used to write shaders. VOPs are wrappers around VEX code snippets.                                                                                                                                                                                                                               |
| CVEX   | **Context agnostic Vector Expression Language.** This has replaced all the VEX specific contexts throughout Houdini. It is a generalized language that uses the same environment and functions anywhere inside Houdini.                                                                                                                            |
| COPs   | **Composite Operators** in composite type folders. Used in image compositing operations.                                                                                                                                                                                                                                                           |
| ROPs   | **Render Operators** in side ROP Output directories which are used to create render output dependency graphs for automating output of any type of data and for triggering external processes like rendering. Commonly used to generate sequences of geometry, simulation data and trigger Render tasks that generates sequences of images to disk. |
| CHOPs  | **Channel Operators** used to create and modify any type of raw channel data from motion to audio and everything in between. Most users safely ignore the CHOP context, and so can you, for now. Put it on the “get to it later” list when learning Houdini. But definitely keep it on the list.                                                   |

## Best practices / Tips

* When using `copytopoint` for an object and a grid, you can attach an `add` node after the grid to delete all unused geometry; leaving only the points.
* With more than one node selected, hold alt/option and drag a new connection. It will automatically create a `merge`node.
* When using the TAB menu to create a node, you can type the initials of the node name to access it. Example:
  * Point wrangle: PW&#x20;
  * Attribute from Map: AFM or AM
