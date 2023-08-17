# Master Properties

### Add Property as Essential Property&#x20;

```javascript
function addToMotionGraphicsTemplate(comp, property) {
    if (property.propertyGroup(1).name === "Effects") {
        var fx = property.property(1);
        fx.addToMotionGraphicsTemplateAs(comp, property.name);
    } else {
        property.addToMotionGraphicsTemplateAs(comp, property.name);
    }
}
```
