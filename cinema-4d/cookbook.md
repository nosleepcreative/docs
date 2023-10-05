# Cookbook

## Unsorted

```python
# Get Active Object
obj = doc.GetActiveObject
```

## Matrix Array Transformation

#### Theory

### Position

**Selecting a single element**

```python
n = 20

# Position: Vector to Real
x = marr[n].off.x 
y = 20
z = marr[n].off.z

marr[n].off = c4d.Vector(x,y,z)
```

**Selecting a single element**

```python
for i in range(cnt):
  x = marr[i].off.x 
  y = 20+i*5
  z = marr[i].off.z
  
marr[i].off = c4d.Vector(x,y,z)
```

### Rotation

#### Single Axis

```python

rot_x = c4d.utils.MatrixRotX(c4d.utils.Rad(45))
rot_y = c4d.utils.MatrixRotY(c4d.utils.Rad(30))
rot_z = c4d.utils.MatrixRotZ(c4d.utils.Rad(45))

marr[6] *= rot_x
   
```

#### Multiple Axes with HPB to Matrix

```python
r_x = c4d.utils.Rad(11)
r_y = 0
r_z = c4d.utils.Rad(18)

vect = c4d.Vector(r_x, r_y, r_z)
rotation = c4d.utils.HPBToMatrix(vect,5)

marr[6] *= rotation
```

### Scale

```python
for i in range(cnt):
    x = random.uniform(0.2,1) 
    y = random.uniform(0.2,1)
    z = random.uniform(0.2,1)
    vect = c4d.Vector(x,y,z)
  #  marr[i].Scale(float(i/10))
    marr[i].Scale(vect)
```

## Color

<pre class="language-python"><code class="lang-python">carr = moData.GetArray(c4d.MODATA_COLOR) # Color Array
<strong>
</strong><strong># Gray Scale
</strong># carr[0] = c4d.Vector(0.5) 

for i in range(cnt):
    r = random.random()
    g = random.random() 
    b = random.random()
    carr[i] = c4d.Vector(r,g,b)
    
# Update Color Array
moData.SetArray(c4d.MODATA_COLOR, carr, hasField)

</code></pre>

## References

* C4D SDK Documentation
*
* [Cinema 4D Python Bytes](https://www.youtube.com/playlist?list=PLpss88MSwvy5-a\_RU1kHJtDcflY57VW7F)
* [Cinema4D Python SDK](https://developers.maxon.net/docs/Cinema4DPythonSDK/html/manuals/introduction/python\_script\_manager.html)

[C4D Python SDK Extended Github, Plugin Cafe](https://github.com/PluginCafe/cinema4d\_py\_sdk\_extended)[https://github.com/aturtur/cinema4d-scripts](https://github.com/aturtur/cinema4d-scripts)

##

## Formula

Documentation

**Alternate intensity based on row number (Animate over time)**

```jsx
mod((id/5);2)?(t;-t)
```

**Animate over time based on the row number sequence**

```jsx
(id/5)/(count/5)*1.5*t
```
