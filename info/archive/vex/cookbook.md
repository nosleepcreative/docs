# Cookbook

## Generating points

Ensure that `pointwrangle` is set to run over Detail&#x20;

### Stacking boxes

{% tabs %}
{% tab title="pointwrangle" %}
```c
//user controls 
float size = chf("size");
int pt =  chi("numpt");

// OR reference box size with expressions
// float size  = `chs("/obj/Boxes/box4/sizey")`; // notice the backticks for expressions

for(int i =0 ;i<pt;i++){
    float x = 0;
    float y = i*size;
    float z = 0;
    v@loc = set(x,y,z);
    addpoint(0,v@loc);
}
```
{% endtab %}

{% tab title="copystamp" %}
```c
// change center to bottom for SOP
ch("sizey") * .5

//place expresssion into translate Y of a copy stamp node
ch("../box1/sizey") + $CY * ch("../box2/sizey")

// get bounding box og geometry
bbox("../merge1",D_YSIZE)
```
{% endtab %}
{% endtabs %}

### Stacking spheres

{% tabs %}
{% tab title="vex" %}
```c
//user controls 
int pt =  chi("numpt");
float size  = 2*`chs("/obj/SnowMan/sphere1/rady")`*`chs("/obj/SnowMan/sphere1/scale")`;

for(int i =0 ;i<pt;i++){
    float x = 0;
    float y = i*size;
    float z = 0;
    v@loc = set(x,y,z);
    addpoint(0,v@loc);
}
```
{% endtab %}

{% tab title="expressions" %}
```c
// align sphere center to bottom
ch("rady")*ch("scale")

// reference scale
ch("../sphereBase/scale") * .8

// transform / stacking 
ch("../sphereBase/rady") * 2 * ch("../sphereBase/scale")
+ ch("../sphereStomach/rady") * 2 * ch("../sphereStomach/scale")

// using bbox
bbox("../merge1",D_YSIZE)
```
{% endtab %}
{% endtabs %}

### Circle

{% tabs %}
{% tab title="vex" %}
```c
int pt = 18;
float angle = 360/pt;
float radius = 20;

for (int i = 0; i < pt; i++)
{
    float x = radius * cos(radians(angle * i));
    float y = radius * sin(radians(angle * i));
    float z = 0;
    v@loc = set(x, y, z); 
    addpoint(0,v@loc);
} 
```
{% endtab %}

{% tab title="expression" %}
```
// copystamp
10 * cos(10 * $CY)
10 * sin(10*$CY)
```
{% endtab %}
{% endtabs %}

### Spirals&#x20;

{% tabs %}
{% tab title="Constant" %}
```c
int points = chi("points");
float radius = chf("radius");
float freq = chf("freq");
float mul = chf("mul");
vector pos ={0,0,0};


pos.x = radius*sin(@Time*freq);
pos.y = radius*cos(@Time*freq);
pos.z = @Time*freq*mul;

addpoint(0,pos);
```
{% endtab %}

{% tab title="Regular" %}
{% code title="Source: David Kahl Polar Coordinates in Houdini" %}
```c
// 1st point wrangle

int points =chi("points");
float step = (PI*2)/ ch("steps");

vector pos;
float angle = chf("angle");
float radius = chf("radius");


for(int i=0; i<points;i++){
    angle+= step;
    radius = float(i)/ float(points);
    pos.x = cos(angle) * radius;
    pos.z = sin(angle) * radius;
    addpoint(0,pos);
}

// 2nd point wrangle
float norm = float(@ptnum)/float(npoints(0));
@P.y=norm*chi("mult");

// 3rd point wrangle
for(int i= 0;i<npoints(0);i++){
    int prim = addprim(0,"polyline");
    addvertex(0,prim,i);
    addvertex(0,prim,i+1);
    
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Phyllotaxis

* [Phyllotactic wrangle nodes examples](http://deborahrfowler.com/HoudiniResources/WrangleNodeExampleVexFunctions.html), Deborah Fowler
  * [http://deborahrfowler.com/MathForVSFX/Phyllotaxis.html](http://deborahrfowler.com/MathForVSFX/Phyllotaxis.html)
  * [http://deborahrfowler.com/MathForVSFX/PhyllotacticZoetrope.html](http://deborahrfowler.com/MathForVSFX/PhyllotacticZoetrope.html)
* [The Algorithmic Beauty of Plants](http://algorithmicbotany.org/papers/#abop) - chapter 4, Springer-Verlag

#### Vogel’s formula

$$
r = c\sqrt n \\θ = n * 137.508
$$

#### Parametric equations

$$
x =  c \sqrt n*cos ( n * 137.508 )\\y=  c \sqrt n*sin ( n * 137.508 )
$$

{% tabs %}
{% tab title="vex_fowler" %}
```c
// source: deborahrfowler.com

int total = chi("total");
float cval = ch("cval");
float zdepth = ch("zdepth");
float angle = 137.508;

void makephyllo(int total; float cval; float zdepth; float angle){
    float x,y,z;
    vector loc ={0,0,0};
    
    // set up the rotation azis variables to orient objects correctly onto the points
    // to do this, we will associate an orient attribute with each point;
    vector axis = {0,0,1};
    float radrotAngle;
    vector4 orient;

    for(int i =0;i<total;i++){
        x = cval *sqrt(i) * cos(radians(angle*i));
        y = cval *sqrt(i) * sin(radians(angle*i));
        z = i*zdepth;
        loc =set(x,y,z);
        
        // set up rotation - orient attribute
        radrotAngle = radians(angle*i);
        orient = quaternion(radrotAngle,axis);
        addpoint(geoself(),loc);
        
        // note that the addpointattrib creates the attribute, it is necesary to use setpointattrib to write the values
        addpointattrib(geoself(),"orient",orient);
        setpointattrib(geoself(),"orient", i, orient, "set");
        
        }
}
    
makephyllo(total,cval,zdepth,angle);

```
{% endtab %}

{% tab title="vex_kiryha" %}
```c
// Source: https://github.com/kiryha/Houdini/wiki//vex-snippets

int count = chi('points');
float bound = 10.0;
float tau = 6.28318530; // 2*$PI
float phi = (1+ sqrt(5))/2; // Golden ratio = 1.618
float golden_angle = (2 - phi)*tau; // In radians(*tau)
vector pos = {0,0,0};
float radius = 1.0;
float theta = 0;
int pt;


vector polar_to_cartesian(float theta; float radius){
    return set(cos(theta)*radius, 0, sin(theta)*radius);
}

for (int n=0; n<count; n++){
    radius = bound * pow(float(n)/float(count), ch('power'));
    theta += golden_angle;
    
    pos = polar_to_cartesian(theta, radius);

    // Create UP, pscale and N attr
    pt = addpoint(0, pos);
    setpointattrib(0, "pscale", pt, pow(radius,0.5));
    setpointattrib(0, "N", pt, normalize(-pos));
    setpointattrib(0, "up", pt, set(0,1,0));
}
```
{% endtab %}

{% tab title="exp" %}
```c
//formula
c * sqrt( $CY ) * cos ( $CY * angle )

// with correct values
2 * sqrt( $CY ) * cos( $CY * 137.508 ) i
```
{% endtab %}
{% endtabs %}

$$
x = \rho cos\theta sin\phi\\y = \rho sin\theta sin\phi\\z=\rho cos\phi
$$

### [Torus](https://math.stackexchange.com/questions/324527/do-these-equations-create-a-helix-wrapped-into-a-torus) / Toroidal

```c
```

$$
x=(a+bcosu)cosv 
\\
y=(a+bcosu)sinv\\
z=bsinu
$$

```c
// Attribute wrangle SOP (Detail mode) 

float vel = chf('vel');
int numpt = chi('Points');
float a = ch('a'); // completion
float b = ch('b'); // arc length
float u = ch('v'); // radius
vector pos; 

for(int i=1;i<numpt;i++){

    addpoint(0,pos);
    float offset = @ptnum*vel*i;
    addprim(0,"polyline",i);
    addvertex(0,1,i);
    pos.x = u*cos(a*offset)*sin(b*offset);
    pos.y = u*sin(a*offset)*sin(b*offset);
    pos.z = u*cos(offset*b); 
}
```

{% tabs %}
{% tab title="1" %}
```c
//  Have a geo & scatter sop before the wrangle node

float t = 1.0*@elemnum/@numelem ;

float completion = ch('completion') * 2 * $PI;
float coils = ch('coils');
float R = ch('outerRadius');
float r = ch('innerRadius');

float u = t * completion * coils ;
float v = t * completion ;

float x = cos(v)*(R+r*cos(u));
float y = sin(v)*(R+r*cos(u));
float z = r * sin(u);

@P = set(x,y,z);

//https://berniebernie.fr/wiki/Houdini_VEX
```
{% endtab %}

{% tab title="2" %}
```c

float t = 3.0*@elemnum/@numelem ;

float a = ch('a'); // radius
float b= ch('b'); // inner radius
float u = ch('u')*t; // coils
float v = ch('v')*t; // completion

float x = (a+b*cos(u))*cos(v);
float y = (a+b*cos(u))*sin(v);
float z = b*sin(u);

v@P = set(x,y,z);

//https://math.stackexchange.com/questions/324527/do-these-equations-create-a-helix-wrapped-into-a-torus
```
{% endtab %}
{% endtabs %}

### Mobius strip

$$
x = [ R + s cos(½ t)] cos(t)\\ 
y= [ R + s cos(½ t)] sin (t) \\
z = s sin(½ t)
$$

```c
//  Have a geo & scatter sop before the wrangle node

float completion = ch('completion');
float t = completion*@elemnum/@numelem ;
t += ch('vel');
float R = chf('radius'); 
float s = chf('s');
vector pos = @P;

float x = (R+s*cos(.5*t))*cos(t);
float y = (R+s*cos(.5*t))*sin(t);
float z = s*sin(0.5*t);

@P = set(x,y,z);
//https://berniebernie.fr/wiki/Houdini_VEX
```

Check out: [https://www3.math.tu-berlin.de/geometrie/Lehre/SS17/MathVis/exercise01.pdf](https://www3.math.tu-berlin.de/geometrie/Lehre/SS17/MathVis/exercise01.pdf)

### Cardioid

```c
```

Also check out: [Times Tables, Mandelbrot and the Heart of Mathematics](https://www.youtube.com/watch?v=qhbuKbxJsk8\&feature=youtu.be)



## Points transformation

### Random pscale

{% tabs %}
{% tab title="static" %}
```c
@pscale = rand(@ptnum)
@pscale = fit01(@pscale, ch('min'),ch('max')); // fit within range 
```
{% endtab %}

{% tab title="animated" %}
```c
```
{% endtab %}
{% endtabs %}

### Random delete points/prim/id

```c
if(rand(@ptnum) > ch('threshold') ) {
   removepoint(0,@ptnum);
}

// shorthand
if rand(@pt)<ch('threshold') 
   removepoint(0,@ptnum);
```

### Random 'pushing' along Normal

```c
float factor = fit01(rand(@ptnum),chf('min'),chf('max'));

@N*=ch('scale')*factor;
@N = pow(@N,1.1);
@P= @N;

```

## Rotation

### Rotate to point to center

```c
//orientVector_Lavrenov

@N = normalize(-@P);
v@side= normalize(cross(@up,@N));
float rot_amount = length(@P)*-chf("rotation_mul");

matrix3 m = ident();
rotate(m,rot_amount, @side);
@N = normalize(@N*m);
@up = normalize(@up*m);

```

### Rotation with p@orient

```c
float rotx = ch('rot_x');
float roty = ch('rot_y');
float rotz = ch('rot_z');
 
vector r = set(rotx,roty,rotz);
 
p@orient = eulertoquaternion(radians(r),XFORM_XYZ);
```

### Rotating points with matrix

```c
matrix3 m = ident(); // identity matrix creation
float angle = radians(chf("degrees")); // angles in radians
vector axis = {0,1,0}; // axis to turn

rotate(m,angle,2);
@P *= m;

```

## Scale

### Scale primitive locally with matrix & foreach

{% tabs %}
{% tab title="Local" %}
```c
float scale = chf('scale');
vector nml = prim_normal(0, @primnum, {0,0,0});
int pts[] = primpoints(0, @primnum);
foreach(int pt; pts){
    matrix m = instance(v@P, nml, scale, {0,0,0}, {0,0,0,1}, v@P);
    vector pos = point(0, 'P', pt) * m;
    setpointattrib(0, 'P', pt, pos, 'set');
} 
// Source:https://www.sidefx.com/forum/topic/50477/?page=1#post-227472
```
{% endtab %}

{% tab title="towards Prim Center" %}
```c
float scale = chf('scale');
int pts[] = primpoints(0, @primnum);
foreach(int pt; pts){
    vector pos_pt = point(0, 'P', pt);
    vector dir = normalize(pos_pt - v@P);
    vector pos = pos_pt + dir * scale;
    setpointattrib(0, 'P', pt, pos, 'set');
} 
```
{% endtab %}
{% endtabs %}

## Spreading points in one axis

![](<../../../.gitbook/assets/image (38).png>)

```c
@P.y = normalize(curlnoise(@P+@Time*.02)*0.5);
@pscale = rand(@ptnum);
@Cd = rand(@ptnum);
```

## Color

![](../../../.gitbook/assets/vex\_cd\_bands.gif)

### Band(s) of color moving across geo in one-axis

```c
@dir = @P.y;
float width = chf('width');
float offset = chf('offset');
float vel = chf('vel');
@Cd = sin(offset+width*@dir-@Time*vel);
@pscale = @Cd;
```

## Oscillations

### Sin wave

```c
abs(sin(@Time*rand(@ptnum)+chf('Z')));
```

## Using Cd for alpha

```c
float u  = clamp(@value,,0,1); 
@Alpha = chramp('ramp_value'),u)
```

## Connecting lines

### Plexus — Entagma

```c
float maxdist = chf('max_dist');
int npts[] = nearpoints(0,v@P,maxdist);

removeindex(npts,0);
i[]@npts = npts;

foreach(int npt; npts){
     addprim(0,"polyline",@ptnum,npt);
}
   
```

## Type

### Random character

```c
 \\`int(fit01(rand($F),1,94))` 
 
 // use 65-90 for lower case letters.
 
 // Time Shift SOP
 stamp('../copy1','step',2)
 
 // copystamp SOP
  fit01(rand(@ptnum+$F+22),0,100)
```





