# Sass Mixins

## Inhalt
1. [Beschreibung](#Beschreibung)
1. [Anpassungen](#Anpassungen)
1. [Methoden](#Methoden)
    * [headlines](#headlines)
    * [font-size](#font-size)
    * [mobile](#mobile)
    * [desktop](#desktop)
    * [video-ratio](#video-ratio)
    * [width-based-on-quantity](#width-based-on-quantity)

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

### headlines() <a name="headlines"></a>

Setzte Werte für alle Überschriften Tags.
Erleichtert Schreibarbeit und verbessert die Lesbarkeit.

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

### font-size ($size, $important: 0) <a name="font-size"></a>

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

### mobile ($bp: #{$mixins_default_breakpoint_desktop - 1}px) <a name="mobile"></a>

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

### desktop ($bp: #{$mixins_default_breakpoint_desktop}px) <a name="desktop"></a>

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

___

### video-ratio ($container: '.nv-container') <a name="video-ratio"></a>

    html struktur sollte so aussehen:
   
    <div class="nv-container">
        <iframe></iframe>
    </div>

    nützlich für youtube und andere videos die 16:9 dargestellt werden sollen

Code

```scss
@mixin video-ratio($container: '.nv-container')
{
    #{$container}
    {
        padding-top: calc(100% * (9 / 16));
        position: relative;

        iframe 
        {
            position: absolute;
            width: 100%;
            height: 100%;
            left: 0;
            top: 0;
        }
    }
}
```

___

### width-based-on-quantity ($element, $maxItems: 5, $gap: 0) <a name="width-based-on-quantity"></a>

berechnet die breite eines items anhand der anzahl seiner geschwister
bsp: 

    <div>
        <span>Test</span>
        <span>Test</span>
    </div>

-> span width 50%

Code

```scss
@mixin width-based-on-quantity($element, $maxItems: 5, $gap: 0)
{
    #{$element}:first-child:nth-last-child(1) 
    {
        width: 100%;
        @content;
    }

    @for $i from 2 through $maxItems 
    {
        #{$element}:first-child:nth-last-child(#{$i}),
        #{$element}:first-child:nth-last-child(#{$i}) ~ #{$element} 
        {
            width: calc(100% / #{$i} - #{$gap}px);
            @content;
        }
    }
}
```