# Utilities

## Template

```javascript
// template
var myComp = app.project.activeItem;
var myLayers = myComp.selectedLayers;
var ctrl //= myComp.selectedLayers[0];
////////////////////////////////////////////////////////////////////
```

## Generating random numbers

### Max

```javascript
function getRandNum(max) {
    var x = Math.floor(Math.random() * max);
    return x;
};
```

### range

```javascript
function getRandRange(min, max) {
    return Math.random() * (max - min) + min;
}
```

### Random element from array

```javascript
var item = items[Math.floor(Math.random() * items.length)];
```

### Generating combinations with non-repeating elements

* Will break if caught in infinite loop⚠️

```javascript
var nums = [1, 2, 3, 4, 1, 2, 3, 2, 3, 1]; //all numbers to be randomized
var ranNums = [];
var numLayers = nums.length;
var j = 0;

for (i = numLayers; i > 0; i--) {
    j = Math.floor(Math.random() * i); // rand choice
    
    // non-repeating random choice 
    if (ranNums.length > 0) {
        while (nums[j] == ranNums[ranNums.length - 1]) {
            j = Math.floor(Math.random() * i);
        }
    }
    ranNums.push(nums[j]);
    nums.splice(j, 1);
}

//usage
alert(ranNums)

```

### Trim string

```javascript
function trim(str) {
    return str.replace(/^\s+/, '').replace(/\s+$/, '');
}
```

### Measuring distance between 2 points

```javascript
function distanceVector(v1, v2) {
    var dx = v1[0] - v2[0];
    var dy = v1[1] - v2[1];
    return Math.sqrt(dx * dx + dy * dy);
```

## Removing duplicates in array

### [Compress Array by Peter Kahrel](https://community.adobe.com/t5/indesign/js-how-to-remove-duplicate-items-from-an-array/m-p/3044978)

The **arrayCompress** function is very original, but I am skeptical about its performance on large arrays.

_Also, there is two important issues to mention:_

_1) the original array is not preserved, because **array.sort()** reorders its own elements -- we can fix this using **array.concat().sort()**._

_2) the function does not work if any of the supplied strings already contains **"\r"**._—  Marc Autret

```javascript
function arrayCompress(array){
    var str = array.sort().join('\r')+'\r';
    str = str.replace(/([^\r]+\r)(\1)+/g,'$1');

    str = str.replace(/\r$/,'');
    return str.split('\r');

}
```

### Hash-sieving&#x20;



## Creating

### Null

```javascript

function addNull(myName) {

    try {
        var myNull = myComp.layer(myName)
        myNull.name = myName;

    } catch (e) {
        var myNull = myComp.layers.addNull();
        myNull.name = myName;
        myNull.label = 9; // green

    }
    ctrl = myNull;
    return myNull
}
```

### Slider

```javascript
function addSlider(layer, fxName) {
    try {
        layer.effect(fxName)("Slider")
    } catch (e) {
        efx = layer.property("Effects").addProperty("Slider Control");
        efx.name = fxName.toString()
    }
    return efx
}
```

### effect

```javascript
function addFx(layer, fxName, yourFxName) {
    // eg. addFx(ctrl, "Slider Control", '')
    efx = layer.property("Effects").addProperty(fxName);
    if (yourFxName != '') {
        efx.name = yourFxName.toString()
    }
    return efx
}

```

## Check

### If layer exist

```javascript
function doesLayerExist(comp, myname) {
    for (i = 1; i <= comp.numLayers; i++) {
        if (comp.layer(i).name == myname) {
            alert('it does');
            return true;
            break
        }
    }
    // alert('nope')
    return error;
}
```

### If effect exist in layer

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
