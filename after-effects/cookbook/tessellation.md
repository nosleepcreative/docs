---
description: 'Last update: 8 April 2021'
---

# Tessellation & Tiling

## Tessellation

### Rectangular

```javascript
//Create a null layer at the top named "Start Tiles" with a Slider effect "Columns", 
//and one at the bottom named "End Tiles"

// For Position:
var controlLayer = thisComp.layer("Start Tiles");
var numColumns = Math.floor(thisComp.layer("Start Tiles").effect("Columns")("Slider").value);
var tileIndex = index - controlLayer.index-1;
var columnIndex = tileIndex%numColumns;
var rowIndex = Math.floor(tileIndex/numColumns);
var columnWidth = thisComp.width/numColumns;
var firstTile = thisComp.layer(controlLayer.index+1);
var rowHeight = firstTile.height/firstTile.width*columnWidth;
var xPos = columnWidth*(columnIndex+.5);
var yPos = rowHeight*(rowIndex+.5);[xPos, yPos];

// For Scale:
var controlLayer = thisComp.layer("Start Tiles");
var numColumns = Math.floor(thisComp.layer("Start Tiles").effect("Columns")("Slider").value);
var columnWidth = thisComp.width/numColumns;
var firstTile = thisComp.layer(controlLayer.index+1);
var rowHeight = firstTile.width/firstTile.height*columnWidth;
var xyScale = columnWidth/width*100;[xyScale, xyScale]
```

### Hexagonal

$$
height-to-width\ ratio\ of \ regular \  hexagon= 1:1.1547005
$$

```javascript
// POSITION Setup     
var controlLayer = thisComp.layer("Start Tile");    
var numColumns = Math.floor(thisComp.layer("Start Tile").effect("Columns")("Slider").value);    var Mmargins = Math.floor(thisComp.layer("Start Tile").effect("Margins")("Slider").value);    var myWidthRatio = thisComp.layer("Start Tile").effect("Height Adjustment")("Slider");    var myZPos = thisComp.layer("Start Tile").effect("Z-Pos Adjustment")("Slider");    var mySeed = thisComp.layer("Start Tile").effect("Seed")("Slider");    // Indexing     var tileIndex = index - controlLayer.index-1;    var columnIndex = tileIndex%numColumns;    var rowIndex = Math.floor(tileIndex/numColumns);    if (rowIndex % 2 == 0) {var oddEven = 1;}else{oddEven=0;}    // Z-Positioning     seedRandom(index+mySeed, true);    var zPos = random(-myZPos,myZPos);    

// Positioning     
var columnWidth = thisComp.width/numColumns ;    
var firstTile = thisComp.layer(controlLayer.index+1);    
var rowHeight = firstTile.height/firstTile.width*columnWidth;    
var xPos = columnWidth*(columnIndex+.5);    
var yPos = rowHeight*(rowIndex+.5);    
[xPos +oddEven*columnWidth/2, yPos*myWidthRatio,zPos];


// 
// SCALE Setup
var controlLayer = thisComp.layer("Start Tile");    
var numColumns = Math.floor(thisComp.layer("Start Tile").effect("Columns")("Slider").value);    
var myScaleRatio = thisComp.layer("Start Tile").effect("Scale Adjustment")("Slider");        

// Indexing     
var columnWidth = thisComp.width/numColumns ;    
var firstTile = thisComp.layer(controlLayer.index+1);    
var rowHeight = firstTile.width/firstTile.height*columnWidth;        


//Scaling     
var xyScale = columnWidth/width*100;    
[xyScale, xyScale]*myScaleRatio;
```

## Layer slider with responsive positioning

![](<../../.gitbook/assets/setup\_ slider\_01.gif>)

**Parameters:**

1. **Layer can be aligned in x-axis with adjustable even space in-between**&#x20;
   1. For that to happen, the anchor points of the layers must be centered
   2. This **prevents inconsistent opacity** for the layers on both sides
2. If a layer scale changes, the spacing should change accordingly
3. Create a control that just change the active "tile";

#### Tiling formula

$$
(target.width/2-space)-(active.width/2)
$$

{% tabs %}
{% tab title="One direction" %}
{% code title="" %}
```javascript
//POSITION

// VARIABLES	
space = 0;
dir = 1; // 1 for tile right, -1 to tile left
axisX = 1; // 1 to turn on, 0 to turn off
axisY = 0; //1 to turn on, 0 to turn off

// SETUP
target = thisComp.layer(index + dir)
tpos = target.transform.position;
tscale = target.transform.scale[0] / 100;
tSrc = thisComp.layer(index + dir).sourceRectAtTime().width / 2 * tscale
tSrcY = thisComp.layer(index + dir).sourceRectAtTime().height / 2 * tscale

s = sourceRectAtTime();
activeWidth = s.width / 2 * transform.scale[0] / 100
activeHeight = s.height / 2 * transform.scale[0] / 100


// EXECUTION: Center position to left of target layer, offset the width, + spacing
tpos += [(activeWidth + tSrc + space) * axisX, (activeHeight + tSrcY + space) * axisY] * dir; 


// OPACITY

minOpacity = 0;
maxDist = thisComp.width/2;

v = transform.position[0] // Get x position
d = Math.abs(length(v, thisComp.width / 2)); // Get distance between layers

ease(d, 0, maxDist, 100, minOpacity)
```
{% endcode %}
{% endtab %}

{% tab title="Two Directions" %}
```javascript
// VARIABLE
space = thisComp.layer("CONTROL").effect("step")("Slider");
center = thisComp.layer("Center");

// SETUP
dir = -1; // Direction for Right 
if (index < center.index) {
    dir = 1;
} // Direction Left if below Center Layer

target = thisComp.layer(index + dir)
tpos = target.transform.position;
tscale = target.transform.scale[0] / 100;
tSrc = thisComp.layer(index + dir).sourceRectAtTime().width / 2 * tscale

s = sourceRectAtTime();
activeWidth = s.width / 2 * transform.scale[0] / 100

// EXECUTE
tpos += [tSrc * dir, 0]; // // Center position to left of target layer 
tpos += [activeWidth * dir, 0] //// Offset the width 
tpos += [space * dir, 0] //add spacing
```
{% endtab %}
{% endtabs %}
