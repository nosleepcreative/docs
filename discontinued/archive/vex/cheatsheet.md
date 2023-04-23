# Cheatsheet

## hscript

#### References

* Sidefx, [Expression cookbook](https://www.sidefx.com/docs/houdini/ref/expression\_cookbook.html)
* Sidefx, [Parameter Expressions](ttps://www.sidefx.com/docs/houdini/network/expressions.html)
* [https://www.sidefx.com/docs/houdini/expressions/index.html](https://www.sidefx.com/docs/houdini/expressions/index.html)

#### Repositories

```c
$CY // copy number    
```



## Data types declaration

```c
int x = 18; // integer
float y =  3.142 // float 
string name = "John";  // string
vector v = {1,1,1};
matrix3 m = ident(); // identity matrix creation
quaternion 

// array form: member_type var_name[]:
float my_array[];
vector_array[];
str_array[];

//global attribute
@myGlobalAttribute
v@myVector = set(-1,-1,-1);
i@var = 1;
```

## Statements

```c
// Loops
for(int i =1; i<10;i++)
    {
}

// if conditional 
if(x==1){
    ...
    }else{
    ...
}

// while 
while(condition){
    yourStatement;
}
```

## Attributes

{% code title="" %}
```c
normalize 
// Position
@P 
@P.x
@P.y
@P.z

// Normal
@N 

// color
@Cd.r
@Cd 
@Cd.g
@Cd.b
@Alpha // Alpha


//scale
@pscale = 1;

@scale.x = 1;
@scale.y = 1;
@scale.z = 5;

// Set scale, and manipulate one axis only
@scale =set(1,1,1); 
@scale.y = 2.

// commonly used
@ptnum
@
```
{% endcode %}

```c
 
// Position
@P 
@P.x
@P.y
@P.z

// Normal
@N 

// color
@Cd.r
@Cd 
@Cd.g
@Cd.b
@Alpha // Alpha


//scaling
@pscale = 1;

@scale.x = 1;
@scale.y = 1;
@scale.z = 5;
    
// Set scale, and manipulate one axis only
@scale =set(1,1,1); 
@scale.y = 2.
```

## Functions

```c
v@myVector = set(-1,-1,-1);

fit01(attribute,minVal,maxVal);
fit(attribute,ominVal,omaxVal,minVal,maxVal);
rand(value);
    
normalize
    
//noise types 
noise 
anoise
snoise 
pnoise 

    
//Copystamp
stamp("../copy1","variable",0)
```

## Expressions

```c
Time — $T / @Time
Frame — $F (int) / $FF (float)
Stamp — stamp("path","variable/channel",defaultValue)
    eg. stamp("../copy1","rotation",25)


//Centroid
$CEX, $CEY , $CEZ

$HIP — Project path
$HIPNAME — HIP project name

// Parsing file name 
name.$F4.jpg // $F4 padding: 0008.jpg
```

## Creating controls

```c
ch('threshold')
chf('threshold')
chi('threshold')
chv('vector_parm)'

float  chramp(string channel, float ramppos)
float  chramp(string channel, float ramppos, float time)
vector  chramp(string channel, float ramppos)
vector  chramp(string channel, float ramppos, float time)
```
