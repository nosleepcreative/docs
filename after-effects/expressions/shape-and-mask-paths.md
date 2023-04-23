# Shape & Mask Paths

## General tips

### Maintain stroke width

```javascript
// from campkeyframe
sf = transform.scale[0]/100; ov = value;nv = ov / sf

// for parented shapes 
value / length(toComp([0,0]), toComp([0.7071,0.7071])) || 0.001;


// https://battleaxe.tumblr.com/post/101945073972/maintain-stroke-weight-expression
```

### Looping paths (loopOut() doesn't work for paths)

{% tabs %}
{% tab title="Pingpong" %}
```javascript
if (numKeys >1 && time > key(numKeys).time){
 t1 = key(1).time;
 t2 = key(numKeys).time;
 span = t2 - t1;
 delta = time - t2;
 seg = Math.floor(delta/span);
 t = delta%span;
 valueAtTime((seg%2) ? (t1 + t) : (t2 - t));
}else
 value
```
{% endtab %}

{% tab title="cycle" %}
```
if (numKeys >1 && time > key(numKeys).time){
 t1 = key(1).time;
 t2 = key(numKeys).time;
 span = t2 - t1;
 delta = time - t2;
 t = delta%span;
 valueAtTime(t1 + t)
}else
 value
```
{% endtab %}
{% endtabs %}

## Accessing Shape parameters

### Shape Property Group and Index

```javascript
// shape group index
thisProperty.propertyGroup(2).propertyIndex // change num accordingly

// using name as index eg. line_1
parseInt(thisProperty.propertyGroup(3).name.split("_")[1]); // method 1
parseInt(content(1).name.split("_")[1]) // method 2
```
