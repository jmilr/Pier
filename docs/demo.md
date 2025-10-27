# Demo playground

The repository ships an `index.html` that doubles as a living style guide. It
exercises the layout patterns, form controls, utilities, and theme switching in
one place.

## Build the CSS

Compile the full bundle and copy it to `dist/pier.css`:

```bash
npm install
npm run build:css
```

This runs Dart Sass against `src/full.scss`, applying both light and dark themes
and generating the utility layers.

## View the demo

Open `index.html` in your browser after running the build. A few tips:

- Toggle the "Toggle theme" button to flip between light and dark tokens.
- Hover and focus the tooltip examples to see the pure CSS pattern.
- Adjust spacing utilities in the "Utilities" section to confirm optional layers
  are compiling correctly.
- Keyboard navigation highlights buttons and inputs with the shared focus ring.

If you are serving the demo via a local web server, the footer will pull the
version number from `package.json`. When opening directly from the file system
that fetch is skipped silently.

## Troubleshooting

- **Sass cannot resolve `pier/_all`.** Ensure your Sass load paths include
  `src/` or import via a relative path.
- **No utilities are generated.** Check that the feature flags in
  `pier/_utilities.scss` are enabled or include the dedicated utility mixins.
- **Dark mode has no effect.** Verify the theme mixin is applied to both
  `:root` and `[data-theme='dark']` in your compiled stylesheet.
