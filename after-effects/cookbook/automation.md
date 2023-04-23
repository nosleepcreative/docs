# Automation

## Spreadsheet to text layers&#x20;

* Refer to CoMotion 2021 title sequence

## Spreadsheet to compositions

{% embed url="https://youtu.be/ZQlgxDSBZwk" %}

## Normalize width of layers

$$
nominalValue/width*100
$$

```javascript
nominal = 100
offset = 900; // connect to slider control
threshold = 0;
//
swidth = thisLayer.sourceRectAtTime().width;
svalue = nominal/swidth;*

// conditional 
if(swidth>threshold){
    [svalue,svalue,svalue]*offset
}

```

```javascript
logo=thisLayer.source.layer(thisLayer.source.numLayers);
sHeight=height/logo.height;
sWidth=width/logo.width;
s=Math.min(sHeight,sWidth);
value*s
```

### [**Normalizing image/logo sizes** ](https://forums.creativecow.net/docs/forums/post.php?forumid=227\&postid=22667\&univpostid=22667\&pview=t)**based on sampling alpha**

$$
normalizedScale = value*(nominalValue/width)
$$

{% tabs %}
{% tab title="width" %}
```javascript
nominalWidth = 200;
leftEdge = 0;

for (i = 0; i <= width; i++){
  temp = sampleImage([i,height/2],[0.5,height/2],true,time);
  if (temp[3] > 0){
    leftEdge = i;
    break;
  }
}

rightEdge = width-1;

for (i = width-1; i >= 0; i--){
  temp = sampleImage([i,height/2],[0.5,height/2],true,time);
  if (temp[3] > 0){
    rightEdge = i;
    break;
  }
}
value*nominalWidth/(rightEdge-leftEdge+1)
// cacheCompareSamplesPerSecond 0
```
{% endtab %}

{% tab title="height" %}
```javascript
nominalHeight = 200;
topEdge = 0;
for (i = 0; i <= height; i++){
  temp = sampleImage([width/2,i],[width/2,0.5],true,time);
  if (temp[3] > 0){
    topEdge = i;
    break;
  }
}
bottomEdge = height-1;
for (i = height-1; i >= 0; i--){
  temp = sampleImage([width/2,i],[width/2,0.5],true,time);
  if (temp[3] > 0){
    bottomEdge = i;
    break;
  }
}

alphaheight = (bottomEdge-topEdge+1); // in pixels 
value*nominalHeight/alphaheight*100/value[1]
```
{% endtab %}

{% tab title="ratio" %}
```javascript
// for logos that are symmetrical
//nominal values;
n1 = 200;
n2 = 400;
n3 = 800;

topEdge = 0;
for (i = 0; i <= height; i++){
  temp = sampleImage([width/2,i],[width/2,0.5],true,time);
  if (temp[3] > 0){
    topEdge = i;
    break;
  }
}

leftEdge = 0;

for (i = 0; i <= width; i++){
  temp = sampleImage([i,height/2],[0.5,height/2],true,time);
  if (temp[3] > 0){
    leftEdge = i;
    break;
  }
}
=
aRatio = leftEdge/topHeight;
if(aRatio<1.1){value*n1/leftEfge
```
{% endtab %}
{% endtabs %}

[**Expressions comment to prevent calculations on every frame**](https://forums.creativecow.net/docs/forums/post.php?forumid=227\&postid=35023\&univpostid=35023\&pview=t)

[**https://aescripts.com/auto-crop/**](https://aescripts.com/auto-crop/)
