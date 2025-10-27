# Pier architecture

Pier is organised into small, explicit Sass modules so you can opt in to only
the layers you need. Each layer builds on the previous one and is exposed via
`@forward` through the package entry point.

## Config

Defined in `src/pier/_theme.config.scss` and `src/pier/_config.scss`. The theme
config file declares the `$pier-theme` map and the `pier-theme()` mixin that
merges overrides. The config module resolves values from that map and exposes
traditional Sass variables (e.g. `$breakpoints`, `$spacers`, `$fonts`) for the
rest of the toolkit.

## Tokens

`src/pier/_tokens.scss` contains the `register()` mixin, which emits CSS custom
properties for colours, spacing units, radii, fonts, and breakpoints. Utility
layers call this mixin automatically, but you can also invoke it directly to
scope tokens or change the variable prefix.

## Core

Core functionality lives in `src/pier/_functions.scss` and `src/pier/_mixins.scss`.
These files expose the math helpers, colour lookups, breakpoint mixins, and
spacing/colour generators that power the rest of Pier. The typography re-export
(`src/pier/_typography.scss`) forwards the font-related mixins for convenient
consumption.

## Layout

`src/pier/_layout.scss` provides composable primitives (`stack`, `cluster`,
`auto-grid`, `container`, `bleed`) that can be used directly or through the
utility generator. They rely on the config layer for spacing, radii, and
breakpoint values.

## Components

Lightweight component styles reside in `src/pier/_buttons.scss`. The bundled
build includes these by default, but you can opt out by compiling from
`src/pier-core.scss` instead.

## Helpers

Utility helpers that don't warrant a dedicated module live in
`src/pier/_helpers.scss`. They provide conveniences such as `visually-hidden`
and `clearfix` that can be mixed into components as needed.

## Utilities

`src/pier/_utilities.scss` wires everything together. Its `generate-utilities()`
mixin outputs Pier's spacing, border, colour, and layout helper classes, as well
as breakpoint-scoped variants. The `src/all.scss` entry point runs this mixin to
produce the default utility bundle.
