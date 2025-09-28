# Pier

> A tiny, customisable Sass toolkit for building layout utilities.

Pier was created as a personal alternative to larger frameworks such as
Bootstrap or Tailwind. It focuses on a handful of mixins that generate grids,
spacing helpers, colour variants, and typography rules from a single settings
file. The framework has not been actively developed since around 2017, so the
project now lives here as an archived, self-contained snapshot.

## Project status

- ✅ **Works with modern Sass** – the codebase still compiles with the
  Dart Sass compiler despite relying on the legacy `@import` syntax.
- ⚠️ **Outdated patterns** – duplicate helper functions, heavy reliance on
  global variables, and pre-flexbox fallbacks remain in the code.
- 🌱 **Room to refine** – the grid, spacing, colour, and typography mixins are
  modular enough to be extracted into future projects if desired.

For a detailed audit of the current source, see
[`docs/ASSESSMENT.md`](docs/ASSESSMENT.md).

## Features

- Dependency-free Sass partials – import only the pieces you want.
- Configurable grid, offset, and breakpoint maps.
- Helper mixins that generate spacing, colour, border, and border-radius
  utilities.
- Type scale utilities driven by configurable ratios and base values.

## Getting started

1. Copy `_pier/` and `_settings.scss` into your project.
2. Update `_settings.scss` to match your design tokens and grid needs.
3. Import `settings.scss` at the top of your main Sass file.
4. Optionally include the helper partials (`_helpers.scss`, `_buttons.scss`,
   etc.) that ship with Pier.

See `_pier/helpers.scss` for usage examples of the mixins and generated
utility classes.

## Utility overview

Pier’s Sass mixins include:

`rem-calc($size)`

Translates pixel size to rems.

```css
    .example{
        margin-left: rem-calc(36 / 2);
        margin-left: 2rem;
    }
```

`color($color,[$tone:'base'])`

Maps colours from `_settings.scss` for use in Sass with simple handles. `$tone`
can be `lighter`, `light`, `dark` or `darker`.

```scss
    .example{
        background: color(primary);
        border-color: color(primary, dark);
    }
```
```css
    .example{
        background: #FEEB5F;
        border-color: #E5D246;
    }
```

`colorSet([$modifier:null],$properties…)`

Generates a set of utility classes for each colour defined in `settings.scss`
(`$colors`). `$modifier` can be `hover`, `active` or `focus`.

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

Generate utility classes for sides, sizes in `_settings.scss` for margin &
padding.

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

Output font size & linehight for specified heading level at specified
breakpoint (optional, can be `small`, `medium` or `large`). `$level` can be
`h1`, `h2`, `h3` , `h4`, `p`.

```css
    .example{
        @include scale($level, small);
    }
```

`size($level)`

Returns font size and line-height for `$level` at 3 breakpoints (`small`,
`medium`, `large`).

`borders()`

Generate utility classes for sides, sizes in `_settings.scss` for borders.
