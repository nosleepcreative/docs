# Pimping up AE

## Resources

#### AE Script Starter Pack

* [FX Console](https://www.videocopilot.net/blog/2018/05/fx-console-updated-to-v1-0-3/)
* [Ease & Whizz](https://aescripts.com/ease-and-wizz/)
* [Laber Maker](https://aescripts.com/label-maker/)
* [Project Cleaner](https://aescripts.com/project-cleaner/)
* [Buttcapper](https://www.battleaxe.co/downloads)
* [RepositionAnchorPoint](https://aescripts.com/repositionanchorpoint/)
* Easecopy

#### Others

* After Effects Output modules

#### NoSleepCreative Expression Starter Pack

* Basic Expression Workshop: [https://youtu.be/aZ5F1eCm428](https://youtu.be/aZ5F1eCm428)
* Expression snippet library: [https://docs.nosleepcreative.com/code/javascript-for-ae/expressions](https://docs.nosleepcreative.com/code/javascript-for-ae/expressions)

#### Recommended Readings

**Expression** **Documentation**

* [**Aenhancers — Expressions**](http://expressions.aenhancers.com/)
* [W3 School Javascript](https://www.w3schools.com/js/js\_object\_definition.asp)
* [**Expression guide**](https://readthedocs.org/projects/after-effects-expressions-guide/downloads/pdf/latest/)
* [**JR Canesto AE Tricks Google Sheets**](https://docs.google.com/spreadsheets/d/1a3ArTUHAJwVi-ObZofvz6IfrKbSGSENlaTIRTs8pAJU/edit#gid=0)

**Tutorials**

* \*\*[Motionscript\*\* by Dan Ebbert](http://www.motionscript.com/)
* [Animoplex](https://www.youtube.com/channel/UCbfz\_keteqaKbpiRiS95Dqg)
* [AE Incredible Expressions Challenge](https://www.youtube.com/playlist?list=PLZAr8tT8TcsRj62nIO7ILCMitj5RKjsMf)

## Installing scripts

* **How to install script & scriptsUI**
  * via AE menu
  * via placing in directory&#x20;
  * via [aescripts + aeplugins manager app](https://aescripts.com/learn/aescripts-aeplugins-manager-app/)
  * practice with:  RepositionAnchorPoint
* **Installing via DMG:**&#x20;
  * fx console - shortcut, saving screenshots, copying to clipboard
* **How to install ZXP extensions with ZXP installer**
  * Install Flow

## Setting up your workspaces



## AE Organization & management

{% hint style="info" %}
Essentially, you want to use the same principles as above: having a consistent folder structure, responsibly naming your files, and reducing project size.
{% endhint %}

### Folder Structures

{% file src="../../../.gitbook/assets/nsc_folderStructure_AE_v1.zip" %}
After Effects Folder Structures
{% endfile %}

### Setting up preferences to auto-load AEP template&#x20;

Under Preferences > New Project  > Choose Project Template > Select AEP to use for startup

![](<../../../.gitbook/assets/image (2) (1).png>)

## After Effects Output Modules (AOM)

```javascript
Rule of thumb: 
prores 422HQ for delivery, 
4444+alpha for video that needs alpha, 
LT if storage space is limited,

mp4: high quality 2 pass encoding 50mbps, max render quality
```

### How to save Render Settings(ars) and Output Modules (aom)

If you want to save a render-settings template for use on another system

* Click the **Save All button in the Render Settings Templates dialog box before you close it**&#x20;
* or, reopen the dialog box later by choosing Edit > Templates > Render Settings).&#x20;
* Save the file in an appropriate location on your hard disk, such as in the After Effects application folder.&#x20;
* All the currently loaded render settings are saved in a file with the .ars extension.&#x20;
* Then, copy this file to the disk of the other system. When you start After Effects on that system, choose Edit > Templates > Render Settings, click the Load button, and select the new .ars file to load the settings you saved.

[**Source**](https://forums.creativecow.net/docs/forums/post.php?forumid=2\&postid=1040525\&univpostid=1040525\&pview=t)

### How to load AOM files

Have a item in the render queue > `Output Module` > `Make Template` > `Load` > Select AOM file

![](<../../../.gitbook/assets/image (15).png>)

{% file src="../../../.gitbook/assets/cm_2020_11_ddu (1) (2).aom" %}
NSC After Effects Output Modules
{% endfile %}

##
