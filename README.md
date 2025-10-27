# Pier

> 🚧 A lightweight & tidy Sass framework

Pier started life as a personal alternative to larger frameworks such as
Bootstrap or Tailwind. The framework focuses on a handful of mixins that
generate grids, spacing helpers, colour variants, and typography rules from a
single theme map. This refresh modernises the module structure, introduces a
first-class configuration layer, and ships with a turn-key bundle for rapid
onboarding.

## Quick start

```bash
npm install github:jmilr/pier
```

Import the pre-bundled stylesheet to emit the reset, utilities, grid helpers,
and button styles in one line:

```scss
@use "pier/all";
```

Prefer to keep the namespace? Alias the package instead:

```scss
@use "pier" as pier;

@include pier.generate-grid();
@include pier.generate-utilities();
```

## Theme overrides

All configurable values (colours, spacing, fonts, radii, breakpoints) live in a
single `$pier-theme` map. Override only the keys you care about by calling the
`pier-theme()` mixin before generating any CSS:

```scss
// _theme.scss
@use "pier" as *;
@forward "pier";

@include pier-theme((
  color-accent: #ff7849,
  space-unit: 0.75rem,
  helpers: (
    brand: #6633ff,
  ),
));

@include generate-grid();
@include generate-utilities();
```

Now import your theme file from your application stylesheet:

```scss
@use "theme" as *;
```

Every config variable also respects `$pier-theme-overrides`, so you can apply
overrides inline when using the one-line bundle:

```scss
@use "pier/all" with (
  $pier-theme-overrides: (
    radius: 0.75rem,
    helpers: (primary: #14213d),
  ),
);
```

## CLI helper

Generate the starter `_theme.scss` (shown above) with zero configuration:

```bash
npx pier init
```

The script creates the file in your current working directory, includes the
package import, and adds commented override examples so you can tweak values
quickly.

## Modular imports

Pier exposes every layer via `@forward` so you can cherry-pick pieces:

```scss
@use "pier/functions" as fn;
@use "pier/layout" as layout;
@use "pier/typography" as type;

.my-card {
  @include layout.stack(fn.spacer(4));
  font-family: fn.font-family(primary);
  @include type.size(h3);
}
```

Prefer to keep bundles lean? Import just the grid utilities without components:

```scss
@use "pier/grid";
@use "pier/utilities" as utilities;

@include grid.generate-grid();
@include utilities.generate-utilities($register-tokens: false);
```

> ⚡️ Performance tip: the `@use "pier/all"` entry point is perfect for
> prototypes. For production builds, assemble a slimmer bundle by importing
> individual modules or compiling from `src/pier-core.scss`.

## Build outputs

Run the Dart Sass build to emit distributable stylesheets:

```bash
npm install
npm run build
```

This produces three files in `dist/`:

- `pier.css` – full bundle (reset, utilities, buttons)
- `pier.min.css` – minified full bundle
- `pier-core.css` – reset + utilities without components

## Further reading

- [`docs/architecture.md`](docs/architecture.md) – overview of the Sass layers
- [`docs/USAGE.md`](docs/USAGE.md) – additional recipes and legacy guidance
- [`docs/ASSESSMENT.md`](docs/ASSESSMENT.md) – audit of the original source
