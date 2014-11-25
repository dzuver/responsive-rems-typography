# Responsive rems typography
---
##Introduction
This repository contains demo page using SCSS mixins for generating font size depending on screen size.

##Browser support
Rem units are supported in all modern browsers. They are ok to use in IE 9+ browsers (see http://caniuse.com/#search=rem). For browsers who don't support this units there is simple fallback with size in pixels.

##How to use
First you define breakpoints and base font size (great read on base font size matter http://csswizardry.com/2011/05/font-sizing-with-rem-could-be-avoided/)
```scss
$break-small: 360px;
$break-large: 768px;
base-font-size: 16;
```
Doing math (calculating rems from desired font size in pixels and browser default font-size). 
```scss
@mixin rem($px, $base){
	font-size: $px + px; // pixel font-size fallback
    font-size: ($px / $base) * 1rem; // rem font-size
}
```
###Example
This mixin above for h1 with desired size of 36px and base font size of 16px will be compiled like this:
```css
h1{ 
    font-size: 36px;
    font-size: 2,25rem;
}
```
## Adding responsiveness
```scss
@mixin respond-to($media, $px, $base-font-size) {
    @if $media == handhelds {
        @media only screen and (max-width: $break-small) { @include rem($px, $base-font-size); }
    }
    @else if $media == medium-screens {
        @media only screen and (min-width: $break-small + 1) and (max-width: $break-large - 1) { @include rem($px, $base-font-size); }
    }
    @else if $media == wide-screens {
        @media only screen and (min-width: $break-large) { @include rem($px, $base-font-size); }
    }
}
```
As you can see I created 3 cases for different screen sizes and in each instance I included rem mixin to calculate rem size.

Finally all you need to do is call this mixin in desired class or element.

```scss
h1 { @include respond-to(handhelds, 30, $base-font-size);  @include respond-to(medium-screens, 38, $base-font-size);  @include respond-to(wide-screens, 42, $base-font-size) }
```
Each of these integers represent the desired size of font in pixels in deifferent screen size.


License
----

MIT
