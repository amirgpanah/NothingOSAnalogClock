# Nothing Analog Clock

A grid-snapped, multi-timezone clock canvas. Drag on the canvas to draw clocks, move and resize them on a snapping grid, switch timezones per clock, and manage the list from a settings sidebar. No build step, no dependencies to install, no backend.

🌐 **Live:** https://amirgpanah.github.io/NothingOSAnalogClock/

## What it does

- **Draw clocks** by dragging on the canvas (marquee); move and resize with handles
- **Grid system** with snap-to-grid, adjustable cell size, and top-left/center origin
- **Per-clock timezones** via custom dropdowns (canvas context menu + sidebar rows)
- **Clock shapes** -- pill or rectangle ticks, animated morph (160ms, matches the switch)
- **Sidebar** with settings, reorderable clock list (pointer-driven live sorting), collapsible to a 108px header
- **Light/dark themes** from Figma-generated design tokens (Tier-0 primitives -> Tier-1 semantic)
- **Superellipse (squircle) corners** where supported, with a halved-radius fallback elsewhere

## Project structure

```
index.html              Markup + the JS clock/grid/marquee engine
styles/
  app.css               Canvas, grid, marquee, clock (ticks/hands/hub/handles), snackbar
  components.css        Shared atoms (icon-btn, switch-indicator) + squircle system
  sidebar.css           The settings panel only
  clock-context-menu.css  The floating per-clock menu
theme/
  theme.css             Single import point for the token layer
  tokens/               Generated from Figma token exports (see theme/README.md)
```

See `theme/README.md` for the file-split rationale and token rules.

## Stack

Vanilla HTML/CSS/JS. No bundler, no framework.

- Icons: [Phosphor Icons](https://github.com/phosphor-icons/homepage) via CDN
- Font: [Inter](https://fonts.google.com/specimen/Inter) (full variable package via `rsms.me`)

## Acknowledgments

Built with [Claude](https://claude.ai) (Anthropic) and the [DeepSeek Harness](https://github.com/deepseek-ai) agent workspace.
