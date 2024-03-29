# Type & Text

## Introduction

A library of After Effects expressions to be used for sourceText property of a Text Layer.



## Repetition

### Repeat input string

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="repeat()" %}
```javascript
n = 10; // number to times to repeat
value.repeat(n)
```
{% endtab %}

{% tab title="for-loop" %}
```javascript
var n = 8; // number of times to repeat
s = myText = value;
for(i=1; i<n; i++) s += myText; 
s;
```
{% endtab %}

{% tab title="vertical" %}
```javascript
n = 8; // connect to a slider 
s = myText = value;
for(i=1; i<n; i++) s += "\r" + myText; 
s;
```
{% endtab %}
{% endtabs %}

### Text Grid - Uniform Repetition

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="repeat()" %}
**Explicit**

```javascript
var s = value;  // Source text
var numColumns = 5;  // Number of columns
var numRows = 10;  // Number of rows

var row = s.repeat(numColumns) + "\r";  
row.repeat(numRows);
```

**Concise**

```javascript
(value.repeat(5) + "\r").repeat(10);
```
{% endtab %}

{% tab title="For-loop " %}
```javascript
// User Input:
var numRows = 10; // Number of rows in the output
var numColumns = 22; // Number of columns in the output
var s = value; // Enter the value to be repeated in each cell

// Seed
var result = "";
var j = 0;
while (j < numRows) {
  var k = 0;
  while (k < numColumns) {
    result += s; // Placeholder for the actual random alphanumeric generation code
    k += 1;
  }
  result += "\r";
  j += 1;
}

result
```
{% endtab %}
{% endtabs %}

### Text Grid - Multiple Line Repetition

This code splits a comma-separated string into an array, then formats it into a text block with rows and columns by repeating each item with added prefixes and suffixes.

{% tabs %}
{% tab title="For Loop" %}
```javascript
const str = value;
const strArr = str.split(",");
const prefix = ""; 
const suffix = " ";
const numColumns = 5;
const numRows = 10;

let result = "";

for (let i = 0; i < numRows; i++) {
    const eleIndex = i % strArr.length;
    result += (prefix+strArr[eleIndex]+suffix).repeat(numColumns) + "\r"; 
}

result;
```
{% endtab %}

{% tab title="repeat()" %}
```javascript
s = value;
strArr = s.split(",");
prefix =" ";
suffix =" ";

numColumns = 5; 
numRows = 10; 

row1 = (prefix + strArr[0] + suffix).repeat(numColumns) + "\r";  
row2 = (prefix + strArr[1] + suffix).repeat(numColumns) + "\r";  
row3 = (prefix + strArr[2] + suffix).repeat(numColumns) + "\r";  

rows = row1 + row2 + row3;
rows.repeat(numRows);
```
{% endtab %}
{% endtabs %}

### Text Grid - Number Sequence

This code creates a string of sequential numbers between a start and end range. The numbers are arranged in rows and columns, and each number can have leading zeros and spaces after it.&#x20;

```javascript
//user variables
var startNum = 0;
var maxNum = 200;
var numCol = 10;
var numZero = 2;
var numSpace = 1;

var s = "";


for (var i = 1; i <= maxNum; i++) {
    // add startNum 
    var n = startNum + i - 1;

    // add zeroes
    for (var j = 1; j <= numZero; j++) {
        if (n < Math.pow(10, j)) s += 0
    }
    // add number to string
    s += n;

    // add spaces 
    for (var j = 0; j < numSpace; j++) s += ' '

    // add line break 
    i % numCol == 0 ? s += '\n' : s

}
```

### Text Grid - Random Letter

This function generates a grid of random letters, and the user specify the total number of letters and letters per row.

```javascript
function genLetter() {
    r = random(65, 90); //from a to z
    return String.fromCharCode(r);
}

function randAlphabet(maxNum, col, seed) {
    seedRandom(seed, true);
    var s = "";
    for (i = 1; i <= maxNum; i++) {
        s += genLetter() + ' ';
        if (i % col == 0) s += '\n'; // add line break
    }
    return s
}
randAlphabet(500, 25, 1)
```

### Text Grid - Random Binary&#x20;

![](../../.gitbook/assets/binaryGenerate.jpg)

{% tabs %}
{% tab title="1" %}
```javascript
function binary(maxNum, col, seed) {
    seedRandom(seed, true);
    var s = "";
    for (var i = 1; i <= maxNum; i++) { 
        s += Math.round(random()) + ' ';
        if (i % col == 0) s += '\n'; 
    }
    return s;
}

// Usage
binary(500, 25, 1);
```
{% endtab %}

{% tab title="2" %}
```javascript
n = 300; // connect to slider
seedRandom(seed,true);
let m = b = '';
for(i=0;i<n;i++){
	seedRandom(i+seed,true);
	b = Math.round(random(1)).toString()
	m +=b;
}
```
{% endtab %}
{% endtabs %}

***

## Randomization

### Random Letter

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Solution 1" %}
{% code lineNumbers="true" fullWidth="true" %}
```javascript
// User Input
var numOfLetters = 10; // Modify the number of letters to generate
var useSpaces = true; // Modify to include spaces between letters (true) or not (false)
var changeEveryFrame = false; // Modify if the generated letters should change every frame

// Don’t modify below this line
seedRandom(index, !changeEveryFrame);

function genLetter() {
  var r = random(65, 90); // Generate a random number representing a letter (ASCII code for A to Z)
  return String.fromCharCode(r); // Convert the number to the corresponding letter character
}

var result = "";
for (var i = 0; i < numOfLetters; i++) {
  result += genLetter();
  if (useSpaces) {
    result += " "; // Add a space between letters if useSpaces is true
  }
}
result; 

//source: https://creativecow.net/forums/thread/random-letters-4/

```
{% endcode %}
{% endtab %}

{% tab title="Solution 2" %}
```javascript
// Number of rows in the output
var numRows = 1;

// Number of characters in each row of the output
var numChars = 5;

// Number of frames to hold the same random seed
var holdFrames = 5;

// Calculate the seed for randomization based on time and holdFrames
var seed = Math.floor(time / (holdFrames * thisComp.frameDuration));
seedRandom(seed, true);

var result = "";
var j = 0;

while (j < numRows) {
  var k = 0;
  
  while (k < numChars) {
    var randomCharCode = Math.floor(random(65, 91)); // Generate random number representing uppercase letter in ASCII
    result += String.fromCharCode(randomCharCode); // Convert random number to corresponding letter character
    k += 1;
  }
  
  result += "\r"; // Add a carriage return at the end of each row
  j += 1;
}

result; // Output the generated string

```
{% endtab %}
{% endtabs %}

### Random Digit

```javascript
seedRandom(10,true);
Math.round(random(9));
```

***

## String Manipulation

### Search and replacing string instances

```javascript
var searchString = /\r/g; // \r: lien break; \g: global flag
var replaceString = "newString";
value.replace(searchString, replaceString);
```

### Parsing Text

#### [Sourcetext from Comp Name](https://zacklovatt.com/split-sourcetext-from-comp-name)

```javascript
// if comp name is "comp_05", to get number use this
thisComp.name.split("_")[1] // replace delimiter based on your needs
```

#### Separating source text line feeds into an array

```javascript
// Method 1 
txt = thisComp.layer("insert Text").text.sourceText;
txt.split("\r")[3]; // Regex

// Method 2:using name as index
txt = thisComp.layer("insert Text").text.sourceText;
myIndex = thisLayer.name;
txt.split("\r")[myIndex];
```

#### [Number from comp name](https://www.w3schools.com/jsref/jsref\_parseint.asp)

```javascript
myNum = parseInt(thisComp.name.split(" ")[1],10);
```

## Numbers

### Rounding numbers

{% tabs %}
{% tab title="to integer" %}
```
// Use any of the following
Math.floor(value);
Math.ceil(value);
```
{% endtab %}

{% tab title="pow" %}
```javascript
x = time;
pow = Math.pow(10,5) // 5 is the number of decimals 
x = Math.round(x*pow)/pow;
```
{% endtab %}

{% tab title="toFixed" %}
```
// apply to sourcetext
x = 2 // number of decimal points
value.toFixed(x);
```
{% endtab %}
{% endtabs %}

### Round up if above threshold

```javascript
function roundSpecific(num,thres){
    dec = num - Math.floor(num)
    if(dec>=thres) {num = Math.ceil(num);
}
return num
}
// usage 
roundSpecific(385.96,.9)
```

### Counter

```javascript
startTime = 0
endTime = 2;
startNum = 0;
endNun = 10000
linear(time,startTime,endTime,startNum,endNum);
```



## Dates

### Current date

```javascript
D = new Date(Date(0));
“” + D.getDate() + “/” + (D.getMonth()+1) + “/” + D.getFullYear()

// get year
D = new Date(Date(0));D.getFullYear()

// get month 
D = new Date(Date(0));D.getMonth()+1

// get day
D = new Date(Date(0)); D.getDate()
```

## Expressions selector

**Recommended readings**

* [ WorkBench 34: Expression Selector Intro](https://www.youtube.com/watch?v=FcSX2Heirko)

### Default

```javascript
selectorValue * textIndex/textTotal
```

### Alternating Effector

```javascript
if(textIndex%2) -100; else 100
```

### [Random ](https://forums.creativecow.net/docs/forums/post.php?forumid=227\&postid=8595\&univpostid=8595\&pview=t)position from textIndex

```javascript
seedRandom(textIndex,true);
random([100,100]);
```

### Select text indexes explicitly; e.g. 1, 3, 7, 14, 22, etc.?

```javascript
If you don't have a lot of numbers, then this works:

if(textIndex === 1 || textIndex ===3) {
 100;
} else {
 0;
}

If you do have a ton of numbers, then this works:

i = [1,3,5,7,10,11];
inArray(i);

function inArray(obj) {
 b = 0;
 for(i = 0; i < obj.length; i++) {
  if(obj[i] === textIndex) {
   b = 100;
   break;
  }
 }
 return b;
}
```

### Sin wave effector \[[source](https://forums.creativecow.net/thread/227/17667)]

```javascript
freq = .5;
selectorValue*Math.sin(time*freq*Math.PI*2 + Math.PI*2* textIndex/textTotal)
```

## Basics

```javascript
// getting the character count
l = thisComp.layer("your text layer").text.sourceText.length;

// getting word count 
l = thisComp.layer("your text layer").text.sourceText;
wordsCount = l.split(/ ,| | \./).length;


// Matching text with regex
thisComp.layer("text").text.sourceText.toLowerCase().match(/\w+\./))

// includes() — determines whether a string contains the characters of a specified strin
var str = "Hello world, welcome to the universe.";
var n = str.includes("world");
```

## Utility Functions

### Find Number of Layers that includes string

```javascript
function findLayerbyName(str) {
    var n = thisComp.numLayers;
    var numMattes = 0;
    for (i = 1; i <= n; i++) {
        thisComp.layer(i).name.includes(str) == 1 ? numMattes += 1 : 0;
    }
    return numMattes
}

findLayerbyName("matte")
```

##

##

## Expression Selector (Regex)

```javascript
https://forums.creativecow.net/thread/227/41461
Oleg Pirogov
https://dribbble.com/zeplin
```

```javascript

var t = text.sourceText;
var regex = /\d[a-z]+(?=,)/g;

function indexMatched(index){
var matched = false;
var match;
var i=[];

while ((match = regex.exec(t)) !== null){
matched |= match.index<index & index<match.index+match[0].length;
i.push([match, match.index, match.index+match[0].length]);
}
return matched;
}

indexMatched(textIndex-1) ? 100 : 0;
```

### [Words inside parentheses ](https://forums.creativecow.net/thread/227/42339)

```javascript
var t = text.sourceText;
var regex = /\(([^)]+)(?=\))/g;

function indexMatched(index){
var matched = false;
var match;

while ((match = regex.exec(t)) !== null){
matched |= match.index<index & index<match.index+match[0].length;
}
return matched;
}

indexMatched(textIndex-1) ? 100 : 0;

```

### Hexcode

```javascript
var t = text.sourceText;
var regex = /[A-Fa-f0-9]{6}/g;

function indexMatched(index){
var matched = false;
var match;

while ((match = regex.exec(t)) !== null){
matched |= match.index<index & index<=match.index+match[0].length;
}
return matched;
}

indexMatched(textIndex) ? 100 : 0;
```
