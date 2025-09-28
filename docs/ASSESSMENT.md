# Pier Framework Audit

_Last reviewed: March 2024_

## Overview

Pier is a compact Sass toolkit built around a few configuration maps in
`_settings.scss`. From those settings it generates:

- a flexbox grid with configurable breakpoints and offsets
- spacing and border utilities
- colour-driven helper classes
- typography scaling via ratio-based maps

The code predates the modern Sass module system, but the mixins and functions
remain expressive and easy to extract into other projects.

## Highlights worth salvaging

| Area | Why it still holds up |
| --- | --- |
| **Grid mixins** (`_pier/_grid.scss`) | Uses flexbox and map-driven configuration, making it easy to trim column counts per breakpoint. |
| **Spacing utilities** (`spacer`, `margin`, `padding` mixins) | Generates directional classes from a single `$spacers` map – a lightweight alternative to full utility frameworks. |
| **Colour helpers** (`color`, `colourSet`) | Provides consistent tone variants and utility class generation from a small palette map. |
| **Typography scale** (`scale`, `size`) | Ratio-based heading and paragraph sizing that adapts across breakpoints. |
| **Radii helper** (`radius`, `radii` mixin) | Simple rem-based radii utilities that align with the rest of the design tokens. |

These pieces can be lifted individually or bundled as a set of mixins inside a
new project. They also provide a practical reference for writing your own
utility generators without reaching for Tailwind/Bootstrap.

## Areas showing their age

- **Legacy `@import` syntax.** Everything relies on the deprecated global Sass
  namespace rather than the newer `@use` / `@forward` module system.
- **Duplicated helpers.** `rem-calc` exists in both `_settings.scss` and
  `_pier/_mixins.scss`, which can cause warnings in stricter build setups.
- **Global maps & naming.** Functions depend on globally scoped `$helpers`,
  `$spacers`, `$borders`, etc. – renaming variables requires touching several
  files.
- **Colour tone logic.** The `color()` function applies the same `scale-color`
  adjustments for `lighter`/`darker`, which may not produce desirable contrast
  for all palettes.
- **Fallback clutter.** Helper classes include float and clearfix utilities that
  modern layouts rarely need. Removing them would make the framework leaner.
- **Missing documentation.** Aside from inline comments, there is no guided
  explanation of how the mixins interplay.

## Suggested polish if you ever revive it

1. **Adopt the module system.** Move shared helpers (e.g. `rem-calc`) into
   dedicated modules and re-export them with `@forward` to avoid duplicates.
2. **Split tokens from generators.** Keep `_settings.scss` for design tokens and
   create a separate entry file that wires up the grid/helpers you want.
3. **Refresh colour utilities.** Consider allowing custom tone maps per colour
   or expose a hook to supply pre-computed variants.
4. **Provide examples.** A simple HTML demo showing the grid, spacing, and
   button helpers would make the framework feel complete.
5. **Add build tooling (optional).** A minimal npm script that compiles the Sass
   once would help future you (or others) validate changes quickly.

## Retirement plan

If you simply want to give Pier a cosy resting place:

- Update the README (done) to mark the project as archived and point to this
  audit.
- Tag a final release, or rename the default branch to `main` with an "archived"
  label in the description.
- Leave the source as-is so others can browse or cherry-pick the mixins.

With these notes in place the project serves as a neat snapshot of your Sass
preferences – ready for nostalgia or for cherry-picking snippets when a future
project needs them.
