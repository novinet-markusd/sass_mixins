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

### headlines () <a name="headlines"></a>

Setzte Styling für alle Überschriften Tags.

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

**Beispiel**

```scss
.text 
{
    @include headlines()
    {
        color: red;
        font-size: 24px;
    }
}
```

___

### font-size ($size, $important: false) <a name="font-size"></a>

Berechnet die Schriftgröße von px zu rem.

WICHTIG:
Bei Aufruf keine Angabe in px, sonst kann rem nicht berechnet werden.

**Code**

```scss
@mixin font-size($size, $important: false)
{
    $value: $size / $mixins_default_font_size;

    @if $important == true
    {
        font-size: #{$value}rem;
    }
    @else
    {
        font-size: #{$value}rem !important;
    }

}
```

**Beispiel**

```scss
.text 
{
    @include font-size(24);
}
```

___

### mobile ($bp: #{$mixins_default_breakpoint_desktop - 1}px) <a name="mobile"></a>

Setze Styling für alle Bildschirmbreiten kleiner als $bp.

**Code**

```scss
@mixin mobile($bp: #{$mixins_default_breakpoint_desktop - 1}px)
{
    @media screen and (max-width: #{$bp})
    {
        @content;
    }
}
```

**Beispiel**

```scss
.image 
{
    width: 50%;

    @include mobile()
    {
        width: 100%;
    }
}
```

___

### desktop ($bp: #{$mixins_default_breakpoint_desktop}px) <a name="desktop"></a>

Setze Styling für alle Bildschirmbreiten größer als $bp.

**Code**

```scss
@mixin desktop($bp: #{$mixins_default_breakpoint_desktop}px)
{
    @media screen and (min-width: #{$bp})
    {
        @content;
    }
}
```

**Beispiel**

```scss
.image 
{
    width: 100%;

    @include desktop()
    {
        width: 50%;
    }
}
```

___

### video-ratio ($container: '.nv-container', $element: 'iframe') <a name="video-ratio"></a>

Erstelle einen Container im Format 16:9.
Nützlich für Videos oder Bilder.

Beispiel HTML-Struktur
   
    <div class="nv-container">
        <iframe></iframe>
    </div>

**Code**

```scss
@mixin video-ratio($container: '.nv-container', $element: 'iframe')
{
    #{$container}
    {
        padding-top: calc(100% * (9 / 16));
        position: relative;

        #{$element} 
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

**Beispiel**

```scss
.module-vidoe 
{
    @include video-ratio;
}
```

___

### width-based-on-quantity ($element, $maxItems: 5, $gap: 0) <a name="width-based-on-quantity"></a>

Berechnet die Breite eines Elements anhand der Anzahl seiner Geschwister.

Beispiel HTML-Struktur:

    <div>
        <span>Test</span>
        <span>Test</span>
    </div>

Das Element "span" ist also 50% breit.

**Code**

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

**Beispiel**

```scss
.module-icons 
{
    @include vwidth-based-on-quantity('.nv-item', 2, 10px);
}
```