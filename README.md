# Pier

> A tiny, customisable Sass toolkit for building layout utilities.

Pier started life as a personal alternative to larger frameworks such as
Bootstrap or Tailwind. The framework focuses on a handful of mixins that
generate grids, spacing helpers, colour variants, and typography rules from a
single settings map. The project is intentionally lightweight, but it now uses
modern Sass modules and ships with a few layout primitives that make it easier
to keep extending.

## Project status

- ✅ **Module-first** – the entire toolkit now uses `@use`/`@forward` instead of
the deprecated global `@import` approach.
- ✅ **Token driven** – design tokens live in a single configurable module and
are exposed as CSS custom properties for runtime tweaks.
- 🌱 **Composable utilities** – grid, spacing, colour, layout and typography
mixins can be cherry-picked or re-exported in other projects.

For a detailed audit of the original source (and the motivation for this
refresh), see [`docs/ASSESSMENT.md`](docs/ASSESSMENT.md).

## Features

- Zero dependencies – import only the pieces you need.
- Configurable grid, offset, and breakpoint maps exposed through modern mixins.
- Helper mixins that generate spacing, colour, border, radius, and container
  utilities.
- A ratio-driven typography scale with optional fluid sizing helpers.
- Layout primitives (`stack`, `cluster`, `auto-grid`, `container`) that cover the
  most common “small-but-clever” patterns found in lean CSS frameworks.
- Token registration helpers that emit design tokens as CSS custom properties,
  including tone variants for every colour helper.
- Automatic CSS custom properties for colours, radii, and spacing tokens.

## Getting started

1. Copy the `source/pier/` directory (and `pier.scss` if you want a single entry
   point) into your project.
2. Configure tokens by loading the config module with overrides:

   ```scss
   // settings.scss inside your project
   @use "pier/config" with (
     $helpers: (
       default: #fe5d84,
       primary: #03080a,
       secondary: #ffffff,
       info: (
         base: #3c8ce7,
         light: #4fa3ff,
         dark: #1a5fb4
       )
     ),
     $spacers: (
       0: 0,
       1: 0.5rem,
       2: 0.75rem,
       3: 1rem,
       4: 1.5rem
     )
   );

   @forward "pier";
   @use "pier/grid" as grid;
   @use "pier/utilities" as utilities;

   @include grid.generate-grid();
   @include utilities.generate-utilities();
   ```

3. Import the settings aggregator at the top of your main Sass file and alias it
   however you prefer:

   ```scss
   @use "settings" as pier;

   body {
     font-family: pier.$primary;
     color: pier.color(primary);
   }
   ```

4. Optionally include the helper partials (`_buttons.scss`, etc.) that ship with
   Pier – they already `@use` the settings aggregator.

   ```scss
   @use "pier/tokens" as tokens;

   // Publish tokens without generating any utility classes.
   @include tokens.register(".design-system");
   ```

   The default utility bundle still calls `tokens.register()` internally, but
   the dedicated module makes it easy to scope or rename the CSS custom
   properties that Pier emits.

See `source/pier/_utilities.scss` for the utility classes generated out of the
box, and `source/_buttons.scss` for how the colour helpers compose in practice.

For additional recipes check out [`docs/USAGE.md`](docs/USAGE.md).

## Utility overview

`pier.rem-calc($size)`

Translates pixel size to rems.

`pier.color($token, $tone: base)`

Maps colours from the helpers map. `$tone` can be `lighter`, `light`, `dark`,
`darker`, or `contrast`. Tokens can also be nested maps if you prefer to define
bespoke tone values.

`pier.colour-set([$modifier], $properties...)`

Generates a set of utility classes for each colour defined in the helpers map.
`$modifier` can be `hover`, `focus`, `active`, `before`, `after`, or `disabled`.
Pass a list such as `(border-color, dark)` to pull a specific tone for a given
property.

`pier.margin()` / `pier.padding()`

Generate utility classes for each spacer in the config map. Directional variants
(`x`, `y`, `inline`, `block`, `top`, `right`, `bottom`, `left`) are included.

`pier.size($level)`

Returns font size for `$level` (`h1`, `h2`, `h3`, `h4`, `p`, `small`) across the
configured breakpoints.

`pier.borders()` and `pier.radii()`

Generate utility classes for border widths and radii. Radii values are also
available via `pier.radius($token)` when you need them inline.

`layout.stack($gap)` / `layout.cluster($gap)` / `layout.auto-grid($min, $gap)` /
`layout.container($size)`

Layout primitives that cover stacked flows, wrapping inline clusters, automatic
grids, and responsive containers without relying on legacy float helpers.
