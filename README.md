# Sass Mixins

## Inhalt
1. [Beschreibung](#Beschreibung)
1. [Anpassungen](#Anpassungen)
1. [Methoden](#Methoden)


## Beschreibung

    Ein Repository um hilfreiche Sass Mixins abzulegen, 
    damit man sie bei Projektstart schnell reinkopiern kann.

## Anpassungen

**$mixins_breakpoint_default_desktop (Breakpoint Variable)**

    Für Bootstrap Wert: 992
    Für Uikit Wert: 960

**$mixins_default_font_size (Font Size Variable)**

    Standardmäßig ist das bei Browsern 16px
    Unbedingt ohne px Angabe damit rem berechnung funktioniert

## Methoden

### headlines

**Beschreibung**
    setzte werte für alle headlines
    erleichtert schreibarbeit und verbessert lesbarkeit

**Code**
```scss
@mixin headlines()
{
    h1,h2,h3,h4,h5,h6 
    {
        @content;
    }
}
```