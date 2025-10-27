# Pier architecture

Pier is organised into explicit Sass modules so you can opt in to only the
layers you need. Everything resolves back to the `$pier-theme` map declared in
`src/pier/_theme.config.scss`, and every layer is exported through
`src/_all.scss` for one-line imports.

## Configuration & tokens

- `src/pier/_theme.config.scss` – defines `$pier-theme` and `$pier-theme-dark`,
  plus the `pier-apply-theme()` mixin that emits CSS variables for both base and
  component tokens.
- `src/pier/_config.scss` – resolves theme values into traditional Sass
  variables (`$breakpoints`, `$spacers`, `$fonts`, etc.).
- `src/pier/_tokens.scss` – the `register()` mixin mirrors those tokens into CSS
  custom properties so runtime theme switching works without recompilation.

## Functions & states

- `src/pier/_functions.scss` – colour helpers, spacing utilities, and math
  helpers.
- `src/pier/_mixins.scss` – breakpoint wrappers and the generators used by the
  utility layer.
- `src/pier/_states.scss` – shared focus-ring and interaction mixins plus the
  `.is-*` state classes consumed by buttons and inputs.

## Layout

- `src/pier/_layout.scss` – mixins for `stack`, `cluster`, `sidebar`, `nav`, and
  `cover` patterns.
- `src/pier/_layout.patterns.scss` – class-backed versions of those mixins using
  CSS custom properties for runtime control.
- `src/pier/_grid.scss` – `generate-grid()` still ships responsive column and
  offset helpers.

## Typography

- `src/pier/_typography.scss` – base element styles wired to the fluid type
  scale.
- `src/pier/_typography.roles.scss` – roles (`.lead`, `.small`, `.muted`,
  `.mono`) plus the `pier-text()` mixin for custom slots.

## Components

- `src/pier/_components.tokens.scss` – maps theme tokens to component-specific
  CSS custom properties (buttons, inputs, cards, tooltips).
- `src/pier/_buttons.scss` – semantic button classes with size/state variants.
- `src/pier/_forms.base.scss`, `_forms.inline.scss`, `_forms.feedback.scss` –
  input primitives, inline groups, and validation states.
- `src/pier/_icons.scss` – icon utility classes and placement mixin.
- `src/pier/_tooltips.scss` – attribute-driven tooltip pattern.

## Utilities

- `src/pier/_utilities.scss` – `generate-utilities()` orchestrates spacing,
  colour, and layout helpers. Feature flags allow spacing/alignment/sizing
  utilities to be toggled.
- `src/pier/_utilities.spacing.scss`, `_utilities.align.scss`,
  `_utilities.sizing.scss` – mixins that output each optional utility set.

## Entry points

- `src/_all.scss` – unified forwarder so `@use "pier/_all" as *;` exposes every
  mixin and class.
- `src/pier-core.scss` – reset + utilities (no components) with both themes
  applied.
- `src/full.scss` – full bundle used by the demo and distributable builds.

When adding a new pattern, place the mixin in the appropriate layer and forward
it through `src/_all.scss`. Components should read from the theme maps or
existing CSS variables to stay compatible with light/dark themes.
