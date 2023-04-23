# VSFX 705

## Setting up&#x20;

### Cutter for Mac

#### Modifying the run file&#x20;

```
export PYTHONPATH=$PYTHONPATH:$RMANTREE/bin
export PATH=$RMANTREE/bin:$PATH

export MAYA_USER_DIR=$HOME/Documents/maya
export RMS_SCRIPT_PATHS=$MAYA_USER_DIR/rfm_scripts/image_tool
RMANFB=it

# change directory below to where your cutter is
cd /Users/ddu/Desktop/ddu/projects/vsfx_705/cutter

# To uncomment the next line - remove the '#' character

java -Xms512m -Xmx512m -classpath .:cutter.jar Cutter
```

#### Making the text file executable

```
chmod 777 run
```

### Setting up Maya Env for Mac

[http://fundza.com/rfm/customizing/index.html](http://fundza.com/rfm/customizing/index.html)

1. Copy `rfm_scripts` folder to /Users/ddu/Documents/maya
2. copy `scripts` folder to /Users/ddu/Documents/maya
3. Copy `Arnold Shaders` to /Users/ddu/Documents/maya/projects
4. copy `maya.env` file to /Users/ddu/Library/Preferences/Autodesk/maya/2020

* Maya  > Window > Plugin manager > Ensure Renderman for Maya is loaded and auto-loaded
* check script editor for environment and preferences&#x20;

### Student web spaces

1. Go myScad > [my info](https://my.scad.edu/uPortal/f/my-info/normal/render.uP) > [Web Space Activation](https://sso.scad.edu/ssomanager/c/SSB?pkg=hwskwebs.P\_WebsRegistration)
2. Go to: [https://studentpages.scad.edu/instructions.html](https://studentpages.scad.edu/instructions.html) > Myfile&#x20;
3. Upload your html and asset files to **https://sav-myfile.scad.edu/myfile/ws-idrive/Savannah/Webspaces/Studentpages/web\_pages**

### [Atom](https://www.youtube.com/watch?v=DjEuROpsvp4)

* **Core:** font size: 20, source code pro, 4 spaces tab, Scroll past end&#x20;
* **Packages:** Turn off auto-complete-plus & snippets

```python
apm install script autocomplete-python minimap file-icons python-autopep8 linter-flake8 
maya language-mel
pip install autopep8
pip install flake8 
```

{% hint style="info" %}
if linter does not show up, delete your Atom config files located: `/Users/userName/.atom/config.cson`
{% endhint %}

### **Notes**

```
keep in mind Renderman Attribute Editor, Shelf, Menu bar
```

## Using cutter

* `cmd+click` on a function (eg.print) to read the [**Built-in Functions** ](https://docs.python.org/3.8/library/functions.html)documentation

## Resources

#### Documentation

* [Python built-in functions](https://docs.python.org/3.8/library/functions.html)

#### Learning Python for Maya

* [**Autodesk Introduction to Python Scripting in Maya** ](https://www.youtube.com/watch?v=eXFGeZZbMzQ\&list=PL-4p6ppgFOkWtUtcp46Z\_AufwVP0CougD)
* [Python Scripting for Maya Artists](http://www.chadvernon.com/blog/resources/python-scripting-for-maya-artists/) (on-line), Chad Vernon

#### **Learning Python**

1. [Guru99: Python Tutorial for Beginners](https://www.guru99.com/python-tutorials.html)
2. [Learning Python](http://shop.oreilly.com/product/9780596158071.do), Mark Lutz, O'Reilly Media
3. [Think Python](http://www.greenteapress.com/thinkpython/html/index.html)(on-line), Allen Downey  &#x20;

## Getting started with Python

**Key terms:** list, tuple, dictionary&#x20;

```python
# script is called test.py but it 
# implements a module called "test"
# a modules contrains attributes
# an attribute can be, eg. name of a variable 

# the built-in datatypes are, nubmers, text(string),
# (and collections) list, tuple, dictionary. file.


age = 26
name = "tom"
family = 'jones'
nationatlity = 'welsh'

# an attribute can also be the name of function 
#create function
def person() 
    print(age)
    print(name)
    print(family)

#creating list 
countries = []
countries.append('usa')
countries.append('china')
countries.append('new zealand')
countries.append('england')
#countries.sort() 
#countries.reverse

# using a tuple (fixed value list) - for vertices data structures transfer
locked = (2,4,3,6,8,9)
# i can test my code by printing some value 
# this call the values 
# but comment it out if used asa module
person() 


if __ name__ == '__main__':
    #person() #(debugging purposes) 
    
    #for place in countries:
        # print(place)
    
    #print(countries[3])
    
    print(locked[0])

#print(__name__) # return name of module from where it was run

```

{% tabs %}
{% tab title="fileWriting" %}
```python
# file_test.py
# an example of how to store text in a document 

out_file= open('file directory', 'w')
for n in range(10):
    out_file.write('sphere -r 1;\n)
    out_file.write('move %f %f 0;\n' % (n,(n-2))) # placeholder %
     
out_file.close()

# to run the mel document in Maya use this mel...
#source "filedirectory"
```
{% endtab %}

{% tab title="Python" %}
```python
#vsfx705/cutter/using_test.py
# only possible if the python files exist in the same directory
import test 
from importlib import reload

print(test.nationality)
test.person

```
{% endtab %}

{% tab title="importRandom" %}
```python
# importing random
import random
val = random.uniform(0,1)
print(val)

for n in range(10):
    val = random.uniform(0,1)
    if val>0.5:
        print(val)
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="rib_test" %}
```python
# rib_test.py
"""
Points "P" [0 0 0   3 5 6    5 6 7   9 9 9] "constantwidth" [1.0]
"""
  
import random
  
rib_file = open('/Users/ddu/Desktop/ddu/projects/vsfx_705/cutter/data2.rib', 'w')
  
rib_file.write('##bbox: -5 -5 -5 5 5 5\n')
rib_file.write('Points "P" [\n')
for n in range(100000):
	x = random.uniform(-5, 5)
	y = random.uniform(-5, 5)
	z = random.uniform(-5, 5)
	rib_file.write('%f %f %f\n' % (x,y,z) )
rib_file.write('] "constantwidth" [0.05]')
rib_file.close()

#Maya > Renderman menu > Archive > import rib archive 
```
{% endtab %}

{% tab title="gen_points" %}
```python
# maya/scripts/gen_points.py
  
import random
  
def cubic(num, side):
    data = []
    n = 0
    while n < num:
        x = random.uniform(-side/2, side/2)
        y = random.uniform(-side/2, side/2)
        z = random.uniform(-side/2, side/2)
        data.append( (x,y,z) )
        n = n + 1
    return data
  
def box(num, width, height, depth):
    data = []
    n = 0
    while n < num:
        x = random.uniform(-width/2, width/2)
        y = random.uniform(-height/2, height/2)
        z = random.uniform(-depth/2, depth/2)
        data.append( (x,y,z) )
        n = n + 1
    return data
    
# how to create a spherical point cloud 
def spherical(num,radius):
    pass # define function but not implemented
```
{% endtab %}

{% tab title="rib_particles" %}
```python
# maya/scripts/rib_particles.py
import random
import gen_points
  
rib_file = open('/Users/ddu/Desktop/ddu/projects/vsfx_705/cutter/data2.rib', 'w')
data = gen_points.cubic(10000,10,0.05)
  
rib_file.write('##bbox: -5 -5 -5 5 5 5\n')
rib_file.write('Points "P" [\n')

for coord in data:
	rib_file.write('%f %f %f\n' % (coord[0],coord[1],coord[2]) )
	
rib_file.write('] "constantwidth" [0.05]')
rib_file.close()

#Maya > Renderman menu > Archive > import rib archive 
```
{% endtab %}
{% endtabs %}

```python
questions
    why is my cutter so slow?
    does not have vsfx705
    cannot open hyperlink
```

## Lesson 3

{% tabs %}
{% tab title="recap" %}
```python
list [] 
tuple () fixed values 
## bbox: -5 5 -5 5 5 5 # read by rib

def writeCubic(path

cmd E to render in Renderman

```
{% endtab %}
{% endtabs %}

