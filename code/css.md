# CSS

## [Transparent Sticky Header in WordPress with Elementor](https://www.youtube.com/watch?v=0QpeKGfvKy8)

{% tabs %}
{% tab title="CSS" %}
```css
selector.elementor-sticky--effects{ background-color: rgba(133,130,255,0.5)!important }
selector{ transition: background-color 4s ease !important; }
selector.elementor-sticky--effects >.elementor-container{ min-height: 80px; }
selector > .elementor-container{ transition: min-height 1s ease !important; }
```
{% endtab %}

{% tab title="" %}
```css

selector.elementor-sticky--effects{
   background-color: rgba(0,0,0,0.7)!important
}

selector{
   transition: background-color 1s ease !important;
}

selector.elementor-sticky--effects >.elementor-container{
   min-height: 80px;
}

selector > .elementor-container{
   transition: min-height 1.0s ease !important;
}
```
{% endtab %}
{% endtabs %}

## Elementor

### Custom bullet point spacing

```css
selector ul li {
    margin-bottom: 10px;
}
```

