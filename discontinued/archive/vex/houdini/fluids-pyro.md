# Fluids - Pyro & Smoke

## Recommended Readings



| Items                                                                 | Links                                                                                                                                                                                                                                                                                                              |
| --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Documentation**                                                     | <p></p><ul><li><a href="https://www.sidefx.com/docs/houdini/nodes/dop/pyrosolver.html">Pyro</a><a href="https://www.sidefx.com/docs/houdini/nodes/dop/pyrosolver.html">solver</a></li><li><a href="https://www.sidefx.com/docs/houdini/nodes/dop/pyrosolver_sparse.html">Pyrosolver sparse</a></li></ul>           |
| <p><strong>Industry /</strong> <br><strong>Case-studies</strong> </p> | <ul><li><a href="http://www.tokeru.com/cgwiki/index.php?title=Smoke_and_Pyro">Tokeru </a> - Smoke &#x26; Pyro</li><li><a href="https://vimeo.com/225159293">Pyro Tips &#x26; Tricks // Jeff Wagner // Illume Webina</a>r</li></ul>                                                                                 |
| **Books**                                                             | <ul><li>Fluid Simulation for Computer Graphics, Second Edition</li></ul>                                                                                                                                                                                                                                           |
| **Papers**                                                            | <p></p><ul><li><p><a href="https://www.cs.ubc.ca/~rbridson/fluidsimulation/">Fluid Simulation for Computer Animation //Robert Bridson &#x26; Matthias Müller-Fischer</a></p><ul><li><a href="https://www.cs.ubc.ca/~rbridson/fluidsimulation/fluids_notes.pdf">SIGGRAPH 2007 Course notes</a></li></ul></li></ul> |

## Approach

1. Advect particles  or points (Garbage in garbage out; interesting source interesting output)
2. Convert to **VDB** (stores values where there is one hence faster and cost-effective)
3. Add `DOP` >  Add `smokeobject` + `pyrosolver`
4. Add disturbance or details with microsolvers (Gas `dissipate`, `disturbance`, `turbulence`)
5. Optimize simulation calculation with`gasresizefluiddynamic`
6. Caching simulation
7. Texturing & Rendering

## **Syllabus**

* &#x20;**Kinesthetic learning**
  * Do R\&D on different settings and render them out

##

## Shadow not showing in viewport (not solved)

* Viewport preferences > Under the Effects tab make sure HDR rendering is enabled.&#x20;
* Under the Geometry tab of the Display dialog there is also a Volume Quality drop down.
* Smoke density in smoke

## From Applied Houdini volumes II&#x20;

### Good practice

* **Division sizes:** 150 (sketch), 300 (detailed), 600 (HQ)&#x20;
  * Use Takes to easily toggle values
* Use size of container/division size to get the optimal value for voxel size
* Use **OpenCL** to speed up rendering if you have a good graphics&#x20;
* Override divisions  to about 50 for visualizing guides&#x20;

### Notes

* Temperature is creating velocity
  * Visualize velocity&#x20;
* Gas resize fluid dynamic - have a threshold to cut down on size of bounding box
  * Tracking object - use original&#x20;
* MICROSOLVER
  * gasdissipate&#x20;
  * gasdisturb&#x20;
    * &#x20;Take edges and perturb them
    * prevents mushroom smokes when you disturb the vel
    * control settings - vel
* Rest field
* PRESSURE



## &#x20;Applied Houdini Dynamics III

* **Alternate cloud volume**&#x20;
  * `cloud`
  * `cloudnoise` &#x20;



