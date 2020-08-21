# Sass Mixins

## Inhalt
1. [Beschreibung](#Beschreibung)
1. [Anpassungen](#Anpassungen)
1. [Methoden](#Methoden)
   * [headlines](#headlines)
    * [font-size](#font-size)
  * [mobile](#mobile)
  * [desktop](#desktop)


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

    setzte werte für alle headlines
    erleichtert schreibarbeit und verbessert lesbarkeit

Code

```scss
@mixin headlines()
{
    h1,h2,h3,h4,h5,h6 
    {
        @content;
    }
}
```

___

### font-size

    berechnet die font size von pixel Angabe in rem

    WICHTIG:

    bei Aufruf keine Angabe in px sonst kann rem nicht berechnet werden

Code

```scss
@mixin font-size($size, $important: 0)
{
    $value: $size / $mixins_default_font_size;

    @if $important == 0
    {
        font-size: #{$value}rem;
    }
    @else
    {
        font-size: #{$value}rem !important;
    }

}
```

___

### mobile

    klassischer breakpoint alles unter ... breite

Code

```scss
@mixin mobile($bp: #{$mixins_default_breakpoint_desktop - 1}px)
{
    @media screen and (max-width: #{$bp})
    {
        @content;
    }
}
```

___

### desktop

    klassischer breakpoint alles über ... breite

Code

```scss
@mixin desktop($bp: #{$mixins_default_breakpoint_desktop}px)
{
    @media screen and (min-width: #{$bp})
    {
        @content;
    }
}
```