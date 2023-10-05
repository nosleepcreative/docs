# Maya snippets

## Selection

### Action if selection has item or not

```javascript
import maya.cmds as cmds
target = cmds.ls(sl=True)
if target:
    print('yes')
else:
    print('no')
```

## Adding objects

### To a curve

```javascript
import maya.cmds as cmds
from random import uniform
delta = 1.0/10
for n in range(40):
    if uniform(0,1) > 0.5:
        x,y,z = cmds.pointOnCurve( 'curve44', pr=(delta * n), p=True )
        cmds.sphere(r=uniform(0.01, 0.04))
        cmds.move(x,y,z)
```

```javascript
import maya.cmds as cmds
from random import uniform
delta = 1.0/10
for n in range(40):
    if uniform(0,1) > 0.5:
        x,y,z = cmds.pointOnCurve( 'curve44', pr=(delta * n), p=True )
        cmds.sphere(r=uniform(0.01, 0.04))
        cmds.move(x,y,z)
  
#----------------------------------------
import maya.cmds as cmds
from mesh_utils import *
from random import uniform
  
positions = get_faces_midpoint('pPlane1', False)
for x,y,z in positions:
    inst = cmds.instance('pCone1')[0]
    y_angle = uniform(0, 360)
  
    cmds.rotate(0, y_angle, 0, inst, relative=True)
    cmds.move(x,y,z, inst)
#----------------------------------------
    
```
