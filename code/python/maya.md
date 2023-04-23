# Maya Environment



```
Cam
    opt + LMB - rotate
    opt + RMB - scale
    opt + MMB - move
    
Viewport
    frame geometry - H
    frame selected object - o
    Show Attribute Editor - Ctrl + A
Settings
    preferences - 
    Project - 
    Render -
    
Essential 
    Commander - 
```

## Setting up Visual Studio Code for Maya

{% embed url="https://www.youtube.com/watch?v=sYi1CtKdkow" %}

1. Install Python, Visual Studio Code
2. In VSC, install MEL - Maya Embedded Language, Maya-code, Maya-Py, Maya Code
3. Download latest [devkit](https://www.autodesk.com/developer-network/platform-technologies/maya) > copy devkit into dev kit folder in your Maya application folder&#x20;
4. Modify your JSON&#x20;
5. In Maya > Script Editor > Open ports by entering these code

```javascript
import maya.cmds as cmds
# Open new ports
cmds.commandPort(name=":7001", sourceType="mel", echoOutput=True)
cmds.commandPort(name=":7002", sourceType="python", echoOutput=True)
```

To enable ports at startup create a file named userSetup.mel in the following folder:

```bash
Windows: <drive>:\Documents and Settings\<username>\My Documents\maya\<Version>\scripts
Mac OS X: ~/Library/Preferences/Autodesk/maya/<version>/scripts.
Linux: ~/maya/<version>/scripts.
(where ~ is your home folder)
```

In the userSetup.mel file add the following

```
commandPort -name "localhost:7001" -sourceType "mel" -echoOutput; 
commandPort -name "localhost:7002" -sourceType "python" -echoOutput;
```

```javascript
{
    "python.pythonPath": "python",
    "python.autoComplete.extraPaths": [  "C:/Program Files/Autodesk/Maya2019/devkit/other/pymel/extras/completion/py" ],

}
```

/Applications/Autodesk/maya2020/devkit



## [Autodesk tuts](https://www.youtube.com/watch?v=eXFGeZZbMzQ)

### Part 1: Creating and Manipulating Objects

* open Script Editor to see echo MEL command&#x20;
* go to Help > Python reference&#x20;
* flags: ch,o,w,g,d,name
* DAG - direct acyclic graphic: transform node>shape node > data structures
* Window > Setting / Preferences >  Preferences > Selection > Track Selection Order

Hotkeys

* Cmd T - new python&#x20;

{% tabs %}
{% tab title="keyRotation" %}
```python
import maya.cmds as cmds

def keyFullRotation(pObjectName,pStartTime, pEndTime, pTargetAttribute):

    #print '%s type: %s' % (objectname, objectTypeResult)
    cmds.cutKey(pObjectName, time=(pStartTime,pEndTime), attribute=pTargetAttribute)
    cmds.setKeyframe(pObjectName, time= pStartTime, attribute = pTargetAttribute, value=0)
    cmds.setKeyframe(pObjectName, time= pEndTime, attribute = pTargetAttribute, value=360)
    
    #linear tangent
    cmds.selectKey(pObjectName, time-(pStartTime,pEndTime), attribute = pTargetAttribute
    cmds.keyTangent(inTangentType = 'linear', outTangetType='linear')
    
    
selectionList = cmds.ls(selection=True, type = 'transform))

if len(selectionList)>=1:
    #print 'Selected items: %s' % (selectionList)
    
    for objectName in selectionList:
    
    startTime = cmds.playBackOptions(query=True,minTime=True)
    endTime = cmds.playBackOptions(query=True,maxTime=True)

    #objectTypeResult = cmds.objectType(objectName)
    
    keyFullRotation(objectName, startTime,endTime,'rotateY')
else: 
    print ' Please select at least one object'
```
{% endtab %}

{% tab title="aimAtFirst" %}
```python
#aimAtFirst.py

import maya.cmds. as cmds
selectionList = cmds.ls (orderedSelection = True)

if len(selectionList) >=2:
    print 'Selected itesms: %s' %(selectionList)
    targetName = SelecitonList[0]
    selectionList.remove(targetName)
    
    for objectName in SelectionList:
        print 'Constraining %s towards %s' % (objectName, tartgetName)
        cmds.aimConstraint(targetName, objetName, aimVector = [ 0,1,0])

else:
    print 'Please select two or more objects.'
```
{% endtab %}

{% tab title="randomInstances" %}
```python
#randomInstances.py

import maya.cmds as cmds 
import random

random.seed(1234)

# selectionOrder 
result = cmd.ls(orderedSelection = True)
print 'result: %s' % (result) # replace string technique

transformName = result[0]
# create a group 
instanceGroupName = cmds.group(empty=True,name = transformName + '_instance_grp')

#instancing with for loop
for i in range(0,50):

    instanceResult = cmds.instance(transformName, name = transformName + ' _instance#'
    
    cmds.parent(instanceRsult,instanceGroupName)
    x = random.uniform(10,10)
    y = random.uniform(0,20)
    z = random.uniform(-10,10)

    cmds.move(x,y,z, instanceResult)
    
    #randomize rotation
    xRot= random.uniform (0,360)
    yRot= random.uniform (0,360)
    zRot= random.uniform (0,360)
    cmds.rotation(xRot,yRot,zRot, instanceResult)
    
    # randomize factor
    scalingFactor = random.uniform(0.3, 1.5)
    cmds.scale(scalingFactor, scalingFactor,scalingFactor, instanceResult)

# hide original cube & center pivit
cmds.hide(transformName)
cmds.xform(instanceGroupName, centerPiviots=True)

```
{% endtab %}

{% tab title="randomCubes.py" %}
```python
#randomCubes.py

import maya.cmds as cmds 
import random

random.seed(1234)

#commenting out multiple lines
'''
#fetch all objects who name starts with myCube + wildcard
cubeList = cmds.ls('myCube*') 

#delete all cube items in cubeList
if (len(cubeList)) > 0:
    cmds.delete(cubeList)
'''
    
result = cmds.polyCube(w=9,h=9,d=9, name = 'myCube#')
transformName = result[0]
# create a group 
instanceGroupName = cmds.group(empty=True,name = transformName + '_instance_grp')

#instancing with for loop
for i in range(0,50):

    instanceResult = cmds.instance(transformName, name = transformName + ' _instance#'
    
    cmds.parent(instanceRsult,instanceGroupName)
    x = random.uniform(10,10)
    y = random.uniform(0,20)
    z = random.uniform(-10,10)

    cmds.move(x,y,z, instanceResult)
    
    #randomize rotation
    xRot= random.uniform (0,360)
    yRot= random.uniform (0,360)
    zRot= random.uniform (0,360)
    cmds.rotation(xRot,yRot,zRot, instanceResult)
    
    # randomize factor
    scalingFactor = random.uniform(0.3, 1.5)
    cmds.scale(scalingFactor, scalingFactor,scalingFactor, instanceResult)

# hide original cube & center pivit
cmds.hide(transformName)
cmds.xform(instanceGroupName, centerPiviots=True)

```
{% endtab %}
{% endtabs %}

###

## [Justin Israel: Python for Maya Artists](https://www.youtube.com/watch?v=PDKxDbt6EGQ)

### Why

* widespread
* cross platform&#x20;
* cross-software&#x20;

## Troubleshooting&#x20;

### Modifying userSetup.mel

Mac:  \~/Library/Preferences/Autodesk/maya/2020/scripts





##
