# ScriptUI

## Creating anything

```javascript
//creating a dialog/palette window
var box = new Window('dialog', "title here"); 

// creating a button
box.add('button',undefined, "Close", {name:'title here'});


// creating static text 

// creating a group

// Creating a panel

// Creating
```

### Making dialog box resizable

### Formatting size, alignment

```javascript
"group { \
            orientation:'column', alignment:['fill','top'], \
            header: Group { \
                alignment:['fill','top'], \
                title: StaticText { text:'" + rd_KindaSortaData.scriptName + "', alignment:['fill','center'] }, \
                help: Button { text:'" + rd_KindaSorta_localize(rd_KindaSortaData.strHelp) +"', maximumSize:[30,20], alignment:['right','center'] }, \
            }, \
```

