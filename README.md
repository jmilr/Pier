# Pier

> Light-but-robust Sass primitives for design systems that grow with you.

Pier is a modular Sass framework that compiles alongside your application. It
ships layout mixins, theming hooks, form controls, and component tokens without
forcing a specific runtime. Everything is dependency free and tree-shakeable via
selective `@use` imports.

## Quick start

Install directly from GitHub:

```bash
npm install github:jmilr/pier
```

Drop the unified entry point into your Sass build, apply the default theme, and
emit the grid + utility layers:

```scss
@use "pier/_all" as pier;

@include pier.pier-apply-theme(pier.$pier-theme);
@include pier.pier-apply-theme(pier.$pier-theme-dark, "[data-theme='dark']");
@include pier.generate-grid();
@include pier.generate-utilities();
```

Need fewer layers? Each module is exported individually so you can opt-in to
only the pieces you care about:

```scss
@use "pier/layout" as layout;
@use "pier/forms.base" as forms;

.my-card {
  @include layout.stack(2rem);
  @include forms.pier-input($variant: filled);
}
```

## Theme overrides and dark mode

All tokens live in the `$pier-theme` maps. Override keys via `@use` configuration
or merge them manually before applying the theme mixin:

```scss
@use "pier/_all" as pier with (
  $pier-theme-overrides: (
    color-accent: #ff7849,
    space-unit: 0.75rem,
    components: (
      button: (font-weight: 700),
    ),
  ),
);

@include pier.pier-apply-theme(pier.$pier-theme);
@include pier.pier-apply-theme(pier.$pier-theme-dark, "[data-theme='dark']");
```

Switching to dark mode at runtime only requires toggling the `data-theme`
attribute. Every component reads from CSS custom properties, so the UI updates
without recompilation:

```js
document.documentElement.dataset.theme = 'dark';
```

## Optional utilities

Spacing, alignment, and sizing helpers are generated only when their mixins are
included. Enable or disable them globally by overriding the feature flags in
`pier/_utilities.scss`:

```scss
@use "pier/utilities" with (
  $pier-include-spacing-utilities: false,
  $pier-include-align-utilities: true,
);
```

You can also pull the generators directly:

```scss
@use "pier/utilities.spacing" as spacing;

@include spacing.pier-spacing-utilities((
  0: 0,
  xs: 0.25rem,
  sm: 0.5rem,
));
```

## Bundled builds

The repository ships a couple of ready-made entry points:

- `src/pier-core.scss` – reset, CSS variables, grid, and utilities
- `src/full.scss` – the complete framework including buttons, forms, tooltips, and layout patterns

Compile them with the provided npm scripts (see below) or wire them into your own
build tool.

## Build scripts

```bash
npm install
npm run build:css      # dist/pier.css – full, expanded build
npm run build:css:min  # dist/pier.min.css – minified build
npm run build:core     # dist/pier-core.css – reset + utilities
npm run demo           # build CSS and launch the demo
```

All scripts rely on Dart Sass. Feel free to swap in your own bundler or
integrate these commands into your existing pipeline.

## Documentation

- [`docs/architecture.md`](docs/architecture.md) – layer stack and forwarding strategy
- [`docs/demo.md`](docs/demo.md) – build and explore the living demo
- [`docs/USAGE.md`](docs/USAGE.md) – legacy recipes and additional guidance
