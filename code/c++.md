---
description: For Arnold Render with C++
---

# Shader Dev

#### Tutorials

* [**Compiling Custom Arnold Procedurals (Stand-ins) to Make Mandelbulbs with Maya MtoA, CGStirk**](https://youtu.be/BrZYnjoZLj)
* [https://docs.arnoldrenderer.com/display/A5AFMUG/Technical?preview=%2F40111108%2F40404366%2FArnoldShadersTutorial.pdf](https://docs.arnoldrenderer.com/display/A5AFMUG/Technical?preview=%2F40111108%2F40404366%2FArnoldShadersTutorial.pdf)
*   [https://docs.arnoldrenderer.com/display/A5AFMUG/Creating+a+Shader](https://docs.arnoldrenderer.com/display/A5AFMUG/Creating+a+Shader)

    [https://docs.arnoldrenderer.com/display/A5ARP/Creating+a+Simple+Plugin](https://docs.arnoldrenderer.com/display/A5ARP/Creating+a+Simple+Plugin)



#### Books

* https://thebookofshaders.com/

## Setting up

1. Download VSC
2. Download Arnold SDK

## Setting up Visual Studio Code

{% embed url="https://youtu.be/DIw02CaEusY?t=583" %}

## **Creating the Maya interface for your shader**

### Referencing your template files

1. Use the template from [Arnold docs](https://docs.arnoldrenderer.com/display/A5AFMUG/Creating+a+Shader)
2. Open your Maya env file located in `~/Library/Preferences/Autodesk/maya/2020/`
3. Insert this line at the end and save the file

```
MTOA_TEMPLATES_PATH = $HOME/Documents/maya/projects/arnold
```

{% hint style="info" %}
#### In Professor Kesson's Cutter script editor v8.34 and above, it will automate the process of parsing your cpp file for the node parameters, and write into a python template file.
{% endhint %}

## Utilities

### Mix

```cpp
AtRGB mix(AtRGB a, AtRGB b, float alpha){
	return a*(1-alpha) +b *alpha;
	}

```
