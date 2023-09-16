# Setup & Rigs

## 🛠 Toolkit or rigs setup Best Practices

![](<../../.gitbook/assets/image (29).png>)

**Objective:** Make the toolkit as **fool-proof** as possible by using proper naming conventions, labeling compositions & layers, write my a readme instructions, making a video tutorial, and master properties arrangement. Fool-proof = intuitive , simplicity, coherent.

Give enough user controls that effectively does the job and not confuse or overwhelm users. AKA "less is more"

#### **Naming conventions**

* use **camelCase** and **underscore** (no spaces) for comp or layer names
* File structure: `_demo`, `builds`, `elements`
* for rig compositions, rename to `build_num` eg. build\_4
* in the comments, you can write a brief description of what the rig do

### L**abeling of layers and compositions**

* `green label` - for compositions / layers that users should modify or use
* `blue label` - secondary stuff for your own development purposes or for users to troubleshoot or their own
* `gray label` for anything that the user should not touch

!["readme" sample from plant rigs](<../../.gitbook/assets/image (3) (1) (1).png>)

### **Writing a user guide or readme**

* in a composition, write a description of what your rig does and instructions on how to use it
* this should be the f**irst composition user see when they open the AEP**

### **Cleaning the project file before delivery 🧹**

* be sure to remove any unused assets that may otherwise confuse the users by using `Reduce Project` or `Collect Project Files`
* close all compositions that will not be use, open all compositions that will be used

### **Other good practice**

* render animated elements used (eg. textures)
* create `demos` or samples of what your toolkit can do to let users know the extent of your setup
* avoid 3rd-party plugins that would be difficult for user to acquire

### **Essential Graphics**

* Create two groups: `design` and `motion`
* the design controls should change the stylization or look; there should not be any keyframes
* as for `motion`, anything that effects a movement for the rig will go here eg. wiggle sliders, duration,

### For users

* communicate bugs or error report

### For Leads checking toolkits

* test if all controls work and `Master Properties` are nested in the composition
* making it simpler to use and lighter to render; keep in mind that users may not be as proficient in AE or expressions. It is
* naming convention

## Spriting / multi-image texturing

### Using string matching&#x20;

{% tabs %}
{% tab title="2020" %}
```javascript
// timeRemapping
var src = thisLayer.source;
var txt = thisComp.layer("file").text.sourceText.toLowerCase();

// loop match
for (i = 1; i < src.numLayers; i++) {
    if (src.layer(i).name.toLowerCase().match(txt)) {
        myLayer = src.layer(i);
        break;
    } else {
        9999 // catch error
    }
}

inP = myLayer.inPoint;
outP = myLayer.outPoint-framesToTime(0);
dur = outP - inP;
linear(time,inPoint,dur,inP,outP)
```
{% endtab %}

{% tab title="2019" %}
```javascript
//timeRemap
framesToTime(effect("frameSelect")("Slider"));


// Slidercontrol
myComp = thisLayer.source;
ext = ""//.png
txt = thisComp.layer("lastName").text.sourceText.toLowerCase();

// loop match
for (i = 1; i < myComp.numLayers; i++) {
    if (myComp.layer(i).name.toLowerCase().match(txt)) {
        i-1 // -1 as time starts from 0 ;
        break;
    } else {
        100 // catch error 
    }
}
```
{% endtab %}
{% endtabs %}

### Text layer as a check

```javascript
t = timeToFrames(time);
t = clamp(t,1,index-1);
thisComp.layer(t+1).name;
```
