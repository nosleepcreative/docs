# Formulas

## Introduction

Here is a page with Cinema 4D Formulas that you can use for Formula Effectors or Fields. Formulas are primarily based on C++ syntax.

## Formula Appendix, [_Maxon Help Guide_](https://help.maxon.net/c4d/2024/en-us/Default.htm#html/6194.html)

Basic

```cpp
px,py,pz - Position
rx,ry,rz - Rotation
sx,sy,sz - Scale

u,v,w - UVW
id - Object Index
count - Object Count

falloff - Falloff weight
t - Project Time[-∞..+∞]
f - Frequency[-∞..+∞]

Conditional
?(a;b)
(3>4)?(10;20)
?(a;b)

Arguments such as mod(a;b) must be separated by a semi-colon or by squared brackets [] (then without curved brackets)

rnd(100) is the same as rnd[100] and rnd(100;234) is the same as rnd([100][234]).
```

**Mathematical Operators**

```plaintext
+	Addition	144 + 14 = 158
-	Subtraction	144 - 14 = 130
*	Multiplication	144 * 2 = 288
/	Division	144 / 12 = 12
(	Left parenthesis	3 + 4 * 2 = 11
```

**Units**

```cpp
km	Kilometer	1km = 1000m
m	Meter	144 - 14 = 130
cm	Centimeter	1cm = 0.01m
mm	Millimeter	1mm = 0.001m
um	Micrometer	1um = 0.000001m
nm	Nanometer	1nm = 0.000000001m
mi	Mile	1mi = 1609.344 m
yd	Yard	1yd = 0.914m
ft	Foot	1ft = 0.305m
in	Inch	1in = 0.025m
B	Frame Number
```

Logical Operators

```cpp
 =	Equal compare	1km = 1000m
==	Equal compare	144 - 14 = 130
>	Greater than	1cm = 0.01m
<	Less than	1mm = 0.001m
>=	Greater than or equal compare	1um = 0.000001m
<=	Less than or equal compare	1nm = 0.000000001m
!=	Not equal compare	1mi = 1609.344 m
!	Not	1yd = 0.914m
|| or. or	Or	1ft = 0.305m
&& or. and	And	1in = 0.025m
&	Bitwise and	 
|	Bitwise or	 
^	Bitwise xor	 
~	Bitwise not	 
?(a; b)	Condition, if statement: a, then b	(3 > 4) ? (10; 20) = 20; kann ebenfalls
so formuliert werden: if(3 > 4; 10; 20)	
```

**Constants**

```cpp
e	The constant e (Euler Number) = 2.71828	 
pi	The constant Pi (circular number) = 3.14159	 
pi05	Half Pi	 
pi2	Double Pi	 
piinv	Inverse Pi	 
pi05inv	Half inverse Pi	 
pi2inv	Double inverse Pi	 

// Functions
sin(a)	Sinus	
cos(a)	Cosinus	 
acos(a)	Arcus cosinus	 
asin(a)	Arcus Sinus	 
tan(a)	Tangent	 
atan(a)	Arcus tangent	 
cosh(a)	Cosinus hyerbolicus	 
sinh(a)	Sinus hyerbolicus	 
tanh(a)	Tangent hyerbolicus	 
floor(a)	Round down	floor(11.8) = 11
ceil(a)	Round up	ceil(11.2) = 12
round(a)	Rund	round(11.8) = 12
abs(a)	Absolute / Value	abs(-11) = 11
sqr(a)	Square exponentiation	sqr(5) = 25
sqrt(a)	Square root	sqrt(49) = 7
exp(a)	Exponential function	exp(5) = 148.41
log10(a)	Logarithm to the base of10	log10(100) = 2
log(a)	Logarithm to the base of e	log(e) = 1
trunc(a)	Truncates a number	trunc(-11.8987) = -11
rnd(a{; b})	Random or 0 and a, opt. b as seed	 
pow(a; b)	Exponentiation	pow(2; 3) = 8
mod(a; b)	Modulo	mod(10; 4) = 2
clamp(a; b; c)	Clamps val. of c or a & b	clamp(2; 6; 10) = 6
min(a; b)	Minimum value a or b	min(4; 7) = 4
max(a; b)	Maximum value a or b	max(4; 7) = 7
(a) << (b)	Bitwise shift to left	1 << 4 = 16
(a) shl
```

## Getting Started

{% embed url="https://youtu.be/pfW2HdjWLqg" %}

## Concepts

White to dark vertical

```cpp
id/count
```

Dark to white center, vertical

```cpp
1 - abs(mod(id/count; 1) - 0.5)*2
```

Dark to white center, horizontal

```cpp
1 - abs(mod(u; 1) - 0.5)*2
```

**Radial - White to Dark Center**

```cpp
sqrt(px*px + py*py + pz*pz)/1000
```

## Formula Library

**Default/Wave**

```cpp
/0.5 + sin( ( subfields + ( id / count ) + d ) * f * 360 ) * 0.5
```

**Alternating Lines**

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

```cpp
mod((id/80);2)?(t*f;-t*f)
```
