# Pier
:construction: Alpha :construction: A lightweight &amp; tidy SASS framework for creating your own helper classes.

Includes:
- Simple grid system with configurable column sizes per breakpoint
- DIY padding & margin utility classes with configurable sizes/options
- DIY border utility classes with configurable sizes/options
- Type scale with configurable ratio
- DIY color utility classes with 4 preset shade variants
- Some helper classes for floats, clearing, text-alignment and more

## Features

- Dependency-free.
- Highly Flexible.
- Teeny tiny.

## Demo

<img src="" alt="">

## Installation

Add `_pier/` and `_settings.scss` in your css directory, @import settings.scss at the top of your main Sass file.

Configure `_settings.scss`.

See `_pier/helpers.scss` for mixin usage examples.

## Usage

# Full Documentation Coming Soon™

`rem-calc($size)`

Translates pixel size to rems.

```css
    margin-left: rem-calc(36 / 2);
    margin-left: 2rem;
```

`color($color,[$tone:'base'])`

Maps colours from `_settings.scss` for use in Sass with simple handles. `$tone` can be `lighter`, `light`, `dark` or `darker`.

```scss
    background: color(primary);
    border-color: color(primary, dark);
```
```css
    background: #FEEB5F;
    border-color: #E5D246;
```

`colorSet([$modifier:null],$properties…)`

Generates a set of utility classes for each colour defined in `settings.scss` (`$colors`). `$modifier` can be `hover`, `active` or `focus`.

```scss
    .btn{
    	@include colorSet(background-color, (border-color dark));
    	@include colorSet(hover, (background-color dark), border-color);
    	@include colorSet(active, (background-color light), border-color);
    }
```
```css
    .btn--primary {
    	background-color: #e6e6e6;
    	border-color: #fff
    }
    
    .btn--primary:hover {
    	background-color: #e6e6e6;
    	border-color: #fff
    }
    
    .btn--primary:active {
    	background-color: #fdefd2;
    	border-color: #fbdda1
    }
```

`margin()` and `padding()`

Generate utility classes for sides, sizes in `_settings.scss` for margin & padding.

```scss
    .margin{
    	@include margin();
    }
```
```css
    .margin--0 { margin: 0 }
    
    .margin--1 { margin: .8rem }
    
    .margin--2 { margin: 2.4rem }
    
    .margin--top--0 { margin-top: 0 }
    
    .margin--top--1 { margin-top: .8rem }
    
    .margin--top--2 { margin-top: 2.4rem }
    
    .margin--bottom--0 { margin-bottom: 0 }
    
    .margin--bottom--1 { margin-bottom: .8rem }
    
    .margin--bottom--2 { margin-bottom: 2.4rem }
```

`scale($level,[$breakpoint: 'small'])`

Output font size & linehight for specified heading level. `$level` can be `h1`, `h2`, `h3` , `h4`, `p`

```css
    @include scale($level, small);
```

`size($level)`

Returns font size and line-height for `$level`.

`borders()`

Generate utility classes for sides, sizes in `_settings.scss` for borders.