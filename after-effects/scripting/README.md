---
description: >-
  Here you will find javascript snippets  that  performs one certain small task
  for learning and application
---

# Scripting

## Recommended Readings

**Repositories**

* [**Kbar Scriplet Github**](https://gist.github.com/search?p=5\&q=%23KBar+%23AfterEffects\&ref=searchresults\&utf8=%E2%9C%93)
* [**Redefinery Scripting Fundamentals**](http://www.redefinery.com/ae/fundamentals/)
* [**http://www.motionscript.com/ae-scripting/pre-comp-to-layer-dur.html**](http://www.motionscript.com/ae-scripting/pre-comp-to-layer-dur.html)

### **Functions**

```javascript
//String
indexOf() // gets index of character
split("delimiter") // Split a string into an array of substrings:
length //Return the number of characters in a string
match // Search a string for "ain":
slice() // remove characters from front

// Arrays 
splice() // add elementsto array
toString() // convert to string 

//REGEX
\t // tab
\n // line
\r // carriage return
\s // whitespace


Ref: https://www.w3schools.com/jsref/jsref_replace.asp
```

## Useful Extendscript references&#x20;

| Item                            | Code                                                              |
| ------------------------------- | ----------------------------------------------------------------- |
| **Alert**                       | alert("This is an alert")                                         |
| **Select**                      | openDialog("Please select files")                                 |
| **Open file**                   | var spreadsheet = File("/Users/ddu/Desktop/spreadsheet.csv");     |
| **Open (Prompt)**               | var spreadsheet = File.openDialog("Please select .csv file");     |
| **Read**                        | var readOK = spreadsheet.open("r");                               |
| **Prompt (with default value)** | var value = prompt("What is the value", 10," This is the title"); |
|                                 |                                                                   |

## Basics

```javascript
// Selection
var proj = app.project;
var myComp = app.project.activeItem; // or use "comp"
var myLayers = myComp.selectedLayers;


// Setting values 
~.property("Position").setValue([120,120]);

// making guide layers
.guideLayer = true;

// adding expressions
var exp = "string of expression";
~.transform.position.expression =exp;
```

## How to use Menu Commands

```javascript
// Using ID number
var inMenuID = 2000;
app.executeCommand(inMenuID);


// Using name
app.executeCommand(app.findMenuCommandId("New Project"));
```

## [Adding](https://ae-scripting.docsforadobe.dev/layers/layercollection/?highlight=addnull)

```javascript
//solid
app.project.item(index).layers.addSolid(color, name, width, height, pixelAspect[, duration])

//null
myNull = app.project.activeItem.layers.addNull(); 


```

### Solid Layer

{% tabs %}
{% tab title="black" %}
```javascript
// Black Solid at Comp size

myComp = app.project.activeItem;
mySolid = myComp.layers.addSolid([0,0,0], "Solid", myComp.width, myComp.height,1);
```
{% endtab %}

{% tab title="comp color" %}
```javascript
// Create solid named background with composition background color

comp_bg = app.project.activeItem.bgColor;
myComp = app.project.activeItem;
mySolid = myComp.layers.addSolid(comp_bg, "BG", myComp.width, myComp.height,1);

```
{% endtab %}

{% tab title="ramp" %}
```javascript
//Create solid named background with a ramp effect

myComp = app.project.activeItem;
app.beginUndoGroup("Add Ramp")
mySolid = myComp.layers.addSolid([0,.8,.4], "BG", myComp.width, myComp.height,1);
mySolid.startTime = 0
myEffect = mySolid.property("Effects").addProperty("Ramp");app.endUndoGroup();
```
{% endtab %}

{% tab title="check error" %}
```javascript
{
	var activeItem = app.project.activeItem;

	if (activeItem == null || !(activeItem instanceof CompItem)) {
		alert("Select a comp before running this script");
	} else {
		// create a red, comp-sized solid layer.
		theSolid = activeItem.layers.addSolid([1,0,0],"Solid Layer", activeItem.width, activeItem.height, 1);

		// find the solid's color array values.
		c = theSolid.source.mainSource.color;

		alert("Created a new solid with color values [" + c[0] + "," + c[1] + "," + c[2] + "]");
	}
}
```
{% endtab %}
{% endtabs %}

### Adjustment Layer

```javascript
// Add Adjustment Layer with Effect.jsx
try{
    var adjLayer = app.project.activeItem.layers.addSolid([0,0,0], "Adjustment Layer", app.project.activeItem.width, app.project.activeItem.height, app.project.activeItem.pixelAspect, app.project.activeItem.duration);
    adjLayer.adjustmentLayer = true;
    adjLayer.effect.addProperty("Curves"); 
    }
catch (e) {
    alert (e);
    }
```

### Text layer

```javascript
app.project.activeItem.layers.addText('sourceText')
myText.property("Source Text").expression = " thisComp.name + \" (\" + (1 + (time/thisComp.frameDuration)) + \")\"  "; //add expression
myText.property("Position").setValue([172, 644]); //set position to lower right corner

//using an array
var content = ['text','text','text'] // read content
for(var i=0; i < content.length; i++){
    app.project.activeItem.layers.addText(content[i]);
}

```

More details:[http://docs.aenhancers.com/layers/textlayer/#textlayer](http://docs.aenhancers.com/layers/textlayer/#textlayer)

### Shape layer&#x20;

```javascript
myComp = app.project.activeItem;
myColor = [0,128,255]; // How to set hex code though? Attached to a global fill?

// Create shape layer
var myShapeLayer = myComp.layers.addShape();
myShapeLayer.name = ("minRect");

// Create shape layer & shape (Ellipse, Rect,)
var shapeGroup = myShapeLayer.property("Contents").addProperty("ADBE Vector Group");
var myRect = shapeGroup.property("Contents").addProperty("ADBE Vector Shape - Rect"); //
myRect.property("Size").setValue([300,100]);

// Create stroke properties
var myStroke = shapeGroup.property("Contents").addProperty("ADBE Vector Graphic - Stroke");
myStroke.property("Color").setValue(myColor);
myStroke.property("Opacity").setValue([100]);
myStroke.property("Stroke Width").setValue([2]);


// Create fill
var myFill = shapeGroup.property("Contents").addProperty("ADBE Vector Graphic - Fill");
myFill.property("Color").setValue(myColor);
myFill.property("Opacity").setValue([100]);
var myRepeater = shapeGroup.property("Contents").addProperty("ADBE Vector Filter - Repeater");

// Source: https://forums.creativecow.net/docs/forums/post.php?forumid=227&postid=28156&univpostid=28156&pview=t
```

### Creating a hyperlink&#x20;

```javascript
// Source: https://stackoverflow.com/questions/17665920/open-web-page-in-after-effects-with-extendscript

// checking that the script can access the network:

if (app.preferences.getPrefAsLong("Main Pref Section", "Pref_SCRIPTING_FILE_NETWORK_SECURITY") != 1) {
    alert("Please tick the \"Allow Scripts to Write Files and Access Network\" checkbox if Preferences > General");

    // Then open Preferences > General to let people tick the checkbox
    app.executeCommand(2359);

    // Here you should check again if they ticked it, and choose to continue or stop ...
}
// checking of the OS:

var os = system.osName;
if (!os.length) {
    // I never remember which one is available, but I think $.os always is, you'll have to check
    os = $.os;
}
app_os = (os.indexOf("Win") != -1) ? "Win" : "Mac"

//os-dependent system calls:

var url = "http://aescripts.com";

if (app_os == "Win") {
    system.callSystem("explorer " + url);
} else {
    system.callSystem("open " + url);
}
```

## Folder creation

{% tabs %}
{% tab title="basics" %}
```javascript
//create a single folder
 app.project.items.addFolder("foldername);
 
 // create a folder set
var topFolder = app.project.items.addFolder("Top Level");
topFolder.parentFolder = app.project.rootFolder;
var subFolder = app.project.items.addFolder("Sub Level");
subFolder.parentFolder = topFolder;


// number of items in project panel
app.project.items.length
```
{% endtab %}

{% tab title="parentFolders" %}
```javascript
// Put comma between folder names & NO space between
var str = "output,main_comps,precomps,assets,reference";
var arr = str.split(",");

//Create parent folders
for (i = 0; i < arr.length; i++) {
    app.project.items.addFolder("0" + i + "_" + arr[i].toString().toUpperCase());
}
```
{% endtab %}

{% tab title="createChildFolder" %}
```javascript
// Put comma between folder names & NO space between
var str = "output,main_comps,precomps,assets,reference";
var arr = str.split(",");

//Create parent folders
for (i = 0; i < arr.length; i++) {
    app.project.items.addFolder("0" + i + "_" + arr[i].toString().toUpperCase());
}
app.project.items.addFolder("Ω MESSY");

// Create subfolders using loop
var subfoldersStr = "a_LOGO,b_PHOTOGRAPHY,c_FOOTAGE,d_MOVS,e_TEXTURES,f_AUDIO"
var subfoldersArr = subfoldersStr.split(",");
for (i = 0; i < subfoldersArr.length; i++) {
    var assetSub = app.project.items.addFolder(subfoldersArr[i].toString());
    assetSub.parentFolder = app.project.item(4);
}

```
{% endtab %}
{% endtabs %}

## Instance of

```javascript
for (var i=0; i<proj.selection.length; i++)
{
    if (proj.selection[i] instanceof CompItem)
        comps[comps.length] = proj.selection[i];
}
```

## Check if

### [Check if Layer Has Specific Effect Applied To It](https://community.adobe.com/t5/after-effects/check-if-layer-has-specific-effect-applied-to-it/td-p/10116580?page=1)

```javascript
var myLayer = app.project.activeItem.layer(1);
var hasEffect = false;

for (var i = 1; i <= myLayer.property("Effects").numProperties; i++) {
    if (myLayer.property("Effects").property(i).matchName == "ADBE Tile") {
        alert("It does!");
        hasEffect = true;
        break;
    }
}

if (!hasEffect) {
    myLayer.property("Effects").addProperty("ADBE Tile");
}
```

## Limitations

### indexOf()

```javascript
IndexOf is a string function and doesn't work with arrays anywhere.


//Source: https://forums.creativecow.net/docs/forums/post.php?forumid=227&postid=37977&univpostid=37977&pview=t
```

## Removing

### Effects property group \[[1](https://aenhancers.com/viewtopic.php?t=1897)]

{% tabs %}
{% tab title="comp" %}
```javascript
// removes ALL effects from ALL the layers in active composition

var myComp = app.project.activeItem;
var myEffects;

function removeCompFx(){
  for (var i = 1; i <= myComp.numLayers; i++){
    try{
      myEffects = myComp.layer(i).Effects;
      for (j = myEffects.numProperties; j > 0; j--){
        myEffects.property(j).remove();
      }
    }catch(err){
    }
  }
}

app.beginUndoGroup("removeFx");
removeCompFx();
```
{% endtab %}

{% tab title="selected layers" %}
```javascript
// removes ALL effects from SELECTED layers in active composition

var myComp = app.project.activeItem;
var mySelectedLayers = myComp.selectedLayers;
var myEffects;

function removeSelectedLayersFx(){
  for (var i = 0; i < mySelectedLayers.length; i++){
    try{
      myEffects = mySelectedLayers[i].Effects;
      for (j = myEffects.numProperties; j > 0; j--){
        myEffects.property(j).remove();
      }
    }catch(err){
    }
  }
}

app.beginUndoGroup("removeFx");
removeSelectedLayersFx();
```
{% endtab %}
{% endtabs %}

### Expressions

```javascript
```

## Randomize \[[1](https://www.aenhancers.com/viewtopic.php?t=1082#top)]

### Position

```javascript

//Distributes layers in 2D space within comp size
var thisComp = app.project.activeItem;
var myLayers = thisComp.selectedLayers;
var x = thisComp.width;
var y = thisComp.height;
var randX,randY;

function getRndNum(min, max) {
  return Math.random() * (max - min) + min;
}
for(i=0; i<myLayers.length; i++){
  randX = getRndNum(0,x);
  randY = getRndNum(0,y);
  myLayers[i].property("Position").setValue([randX,randY,0]);
  // myLayers[i].property("Position").setValue([x,y])

}

```

## Misc

### [**Change the background color for the active comp**](https://gist.github.com/aescripts/74ba7303530af9fb9766fa6f50cd3cba)

```javascript
/* Changes the background color for the active comp to white. 
Can be customized to any color you'd like by simply changing the [1,1,1] value to reflect the appropriate RGB values...

Example colors:
[0,0,0] = Black
[0.5,0.5,0.5] = Grey
*/

app.project.activeItem.bgColor=[1,1,1];
```

### Duplicate selected n times

{% tabs %}
{% tab title="prompt" %}
```javascript
app.beginUndoGroup("Duplicate Selected Layers");
var comp = app.project.activeItem;
if(comp){
var numCopies = prompt("How many copies?",5);
    if (numCopies){
	for (var i=0; i < comp.selectedLayers.length; i++) {
	for (var j=1; j <= numCopies; j++) {
	comp.selectedLayers[i].duplicate();
			}
		}
	}
}
app.endUndoGroup;
```
{% endtab %}

{% tab title="15" %}
```javascript
app.beginUndoGroup("Duplicate Selected Layers");
var comp = app.project.activeItem;
if(comp){
var numCopies = 15
    if (numCopies){
	for (var i=0; i < comp.selectedLayers.length; i++) {
	for (var j=1; j <= numCopies; j++) {
	comp.selectedLayers[i].duplicate();
			}
		}
	}
}
app.endUndoGroup;
```
{% endtab %}
{% endtabs %}

## Kbar Scriptlets

### Changes selected Solid source's color to white&#x20;

```javascript
{
	var activeItem = app.project.activeItem;

	if (activeItem == null || !(activeItem instanceof CompItem)) {
		alert("Select a comp before running this script");
	} else {
		if (activeItem.selectedLayers.length < 1) {
			alert("Select a solid layer before running this script");
		} else {
			solidLayer = activeItem.selectedLayers[0];
			solidLayer.source.mainSource.color = [1,1,1];
			alert("Changed solid's color to white.");
		}
	}
}
```

Source: Paul Tuersley, [https://aenhancers.com/viewtopic.php?t=65](https://aenhancers.com/viewtopic.php?t=65)&#x20;

### Change comp bg color to black > white > grey

```javascript
myComp = app.project.activeItem
var bg = myComp.bgColor;
var n =0 ;

var baseColor = [0,0,0];
var col_1 = [1,1,1];
var col_2 = [.5,.5,.5];


if(bg[0]==0&&bg[1]==0&&bg[2]==0) {n=1} // black to white
if(bg[0]==1&&bg[1]==1&&bg[2]==1) {n=2} // white to grey
if(bg[0]==.5&&bg[1]==.5&&bg[2]==.5) {n=3} // grey to black


switch(n){
  case 0:
    app.project.activeItem.bgColor = baseColor;
  break;

  case 1:
    app.project.activeItem.bgColor = col_1;
    break;

	case 2:
    app.project.activeItem.bgColor = col_2;
    break;

	case 3:
    app.project.activeItem.bgColor = baseColor;
    break;
}

```

## Arrays

### Shuffle&#x20;

```javascript
function shuffleArray(array) {
    var currentIndex = array.length, temporaryValue, randomIndex;

    // While there remain elements to shuffle...
    while (0 !== currentIndex) {

        // Pick a remaining element...
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;

        // And swap it with the current element.
        temporaryValue = array[currentIndex];
        array[currentIndex] = array[randomIndex];
        array[randomIndex] = temporaryValue;
    }

    return array;
}
```
