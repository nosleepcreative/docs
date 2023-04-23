# Best Practices

{% hint style="success" %}
Professionalism and expertise does not lies in how good you are at a software or the quality in your portfolio, these soft skills such as organization and thoughtfulness factors into a good motion designer.
{% endhint %}

## File Organization & Management

> Good housekeeping rules make collaboration a seamless and enjoyable experience.

{% hint style="info" %}
**Why is important?**

1. **Team-level** people do not need spend time looking for the right comps or assets, unified system of how to make sense of project files and their elements, avoid confusion \

2. **Personal-level** curation - never fret where your files are , easy access for reel editing or upload, avoid duplicates and reduce storage space usage, cleanliness \

3. **Desmond-level:** I hate unorganized people
{% endhint %}

Since my journey in digital media in 2010, the most efficient and optimal file folder structure I have used is the one from WarnerMedia Studios. Working there, we mostly just access just 2 folders: `projects` and `library`. `Projects` contains folders of different projects with a standardized naming convention, and `library` is a folder filled with assets such as textures, stock photos, 3D models, and so on. I used to separate project folders based on "personal" and "professional" but then I realized it was better to just combine them.

```
root
    projects
        project_1 // use "standard" file folder structure below
        project_2
        ...
    lib
    branding
    portfolio
```

### Folder Structures templates

If you are on a mac, you can copy any of the snippets below to create a folder structure on your desktop. Alternatively, you can download zip files&#x20;

#### HOME — Database

{% tabs %}
{% tab title="v2" %}
```bash
cd ~/desktop
mkdir home
cd home

mkdir -p data/{00_passport_photo,01_id,02_employment,03_studies,04_immigration,05_tax,06_housing,07_insurance,receipt}
mkdir -p portfolio/{_final_delivery,footage/{2020,2019,2018,2017},lib/{01_logos,02_photography,03_footage,04_movs,05_textures,06_3DModels,07_audio,08_fonts},working_file}
mkdir -p 'projects'/DATE_PROJECTNAME
mkdir -p branding/{_final_delivery,lib/{01_photo,02_featured,03_accolades,04_references},working_files}
mkdir -p 'Ω UNSORTED'
```
{% endtab %}

{% tab title="v1" %}
```bash
cd ~/desktop
mkdir HOME
cd HOME

mkdir -p OUT
mkdir -p DATA/{ID,PASSPORT,IMMIGRATION,PROFILE_PHOTOS,SIGNATURE,TAX,HOUSING,INSURANCE}
mkdir -p PORTFOLIO
mkdir -p 'PROJECT — PRO'
mkdir -p 'PROJECT — PERSONAL'/DATE_PROJECTNAME
mkdir -p 'Ω UNSORTED'
```
{% endtab %}
{% endtabs %}

#### For Projects

{% tabs %}
{% tab title="small" %}
```bash
cd ~/desktop
mkdir project_folder_smallForm
cd project_folder_smallForm

mkdir -p 01_Out
mkdir -p 02_Dailies
mkdir -p 03_Workfiles/AEPs
mkdir -p 04_Assets
mkdir -p Ω_SANDBOX
```
{% endtab %}

{% tab title="standard" %}
```bash
cd ~/desktop
mkdir project_DVFX
cd project_DVFX

mkdir -p '_final_delivery'
mkdir -p working_files
mkdir -p dailies
mkdir -p 'lib'/{_from_client,_seq,01_logos,02_photography,03_footage,04_movs,05_textures,06_3DModels,07_audio,08_fonts}
```
{% endtab %}

{% tab title="shaw" %}
```
cd ~/desktop
mkdir project_folder
cd project_folder

mkdir -p ELEMENTS/{3D,AUDIO,FONTS,FOOTAGE,RASTER,VECTOR}
mkdir -p DELIVERABLES
mkdir -p PRESENTATION/{00_PDF,01_INDESIGN,02_STYLEFRAMES,03_WIP,04_BTS}
mkdir -p PROJECTS/{AEP,C4D}
mkdir -p REFERENCE
mkdir -p RENDERS
```
{% endtab %}
{% endtabs %}

### File naming conventions

#### Naming Projects&#x20;

As someone who makes tutorials, I use project code to differentiate them.&#x20;

```javascript
//nosleepcreative
ms - masterstudies
exp - expression
gen - generative 
collab - collaboration
cs - carousel

// personal
fl - freelance
```

For one-off projects, I still abbreviate them into project code such as "comotion" to "cm"

### Quick access with [Alfred](https://www.alfredapp.com/)

The major benefit of having a consistent file structure and naming convention is how you can **access your files just by using the keyboard in a second** rather than clicking through a series of folder to get to it. I use a macOs and I make use of this free app called [**Alfred**](https://www.alfredapp.com/) which is basically a faster and customizable version of Spotlight (the search bar).

## How to deliver files&#x20;

When sending files over to your teammates or any other personnel, please make use of the `Reduce Project` feature in AE. This will remove any used assets or compositions

## Optimization & Efficiency

### Workspaces

### Animation Preset

**Why**: to avoid recreating the same things over and over again, it is a good practice to save and curate your commonly used effects and their settings into animation preset. This way you can avoid rewriting expressions, setting keyframes, or applying combination of effects.

As a motion designer, I highly recommend everyone to build their own library of animation presets that will serve as their bag of tricks. **Not sure animation presets but rigs or templates AEPs as well.**

#### How to save animation presets&#x20;

Select the properties / property groups that you want > `animation menu` > `Save as Animation Preset`

![](<../../../.gitbook/assets/image (11).png>)

### How to save Render Settings(ars) and Output Modules (aom)

If you want to save a render-settings template for use on another system

* Cick the **Save All button in the Render Settings Templates dialog box before you close it**&#x20;
* or, reopen the dialog box later by choosing Edit > Templates > Render Settings).&#x20;
* Save the file in an appropriate location on your hard disk, such as in the After Effects application folder.&#x20;
* All the currently loaded render settings are saved in a file with the .ars extension.&#x20;
* Then, copy this file to the disk of the other system. When you start After Effects on that system, choose Edit > Templates > Render Settings, click the Load button, and select the new .ars file to load the settings you saved.

[**Source**](https://forums.creativecow.net/docs/forums/post.php?forumid=2\&postid=1040525\&univpostid=1040525\&pview=t)



### Extensions

### ScriptUIs

### Project scale

Skills: using proxies, internal file marking, and render setting.&#x20;

Editing can become such a pain when things aren't optimized as files get bigger and longer. Some file sizes that are 2-3Gb only actually need to be under 100 Mb. If you set up your files properly so that someone else can use it, your team will love you for it.

**Readings**

* [**10 Tips for Increasing Your Productivity in After Effects**](https://blog.pond5.com/12772-10-tips-for-increasing-productivity-in-after-effects/?fbclid=IwAR3fskQ3c6PKZ2sKcw-bY\_JP6B8EwdFiuC-F6fdn-CQfvUdvj8y9PtgEt8Q)

## Communication

When working with my peers, here are specifications I always provide for their final delivery.

```
specs
    resolution - 1920x1080
    fps
    duration
    codec - prores 422 hq or prores 4444+alpha

Animation
    shading done via rendering/AE post
    specific properities - rot x -90 to 90

project file delivery 
    reduce project
```

## Shortcuts that you should know&#x20;

### Basics

| Command              | Shortcut               |
| -------------------- | ---------------------- |
| Quit                 | Cmd + Q                |
| Close composition    | Cmd + W                |
| New project          | Cmd+Alt+N              |
| New Folder           | ⌥+⇧+⌘+N&#xD;&#x9;&#xD; |
| New Composition      | Cmd+N                  |
| New Adjustment Layer | Cmd + Alt + Y          |
| New solid            | Cmd+Y                  |
| New Null Layer       | Cmd + Alt +Shift + Y   |
|                      |                        |

### Timeline

|                            |                                       |
| -------------------------- | ------------------------------------- |
| Show animated properties   | U                                     |
| Show modified properties   | UU                                    |
| Show Expressions           | EE                                    |
| Replace Footage            | Cmd + Option + H                      |
| Adjust Kerning             | Option (Alt) + Left/ Right Arrow keys |
| Adjust Tracking            | Option (Alt) + Up/Down Arrow keys     |
| Trim comp to in & out      | Cmd+Shift +X                          |
| Trim layer inPoint to CTI  | cmd+ \[                               |
| Trim layer inPoint to CTI  | cmd+ ]                                |
| Render                     | Cmd + Shift + /                       |
| Render Queue               | Opt + Cmd + 0                         |
| New project                | Opt + Cmd + N                         |

```
Collapse layer properties - Shift + ~
```



