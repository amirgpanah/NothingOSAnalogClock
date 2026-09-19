# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Fixed
- Mobile double-tap after swiping the sidebar: canvas `:hover` reveals (resize handles, per-clock menu) are now gated behind `html:not([data-touch])` like the sidebar, so sticky emulated hover on touch can no longer swallow the next tap.
- A tap-revealed clock menu now dismisses when tapping anywhere outside the clock; the outside tap's own click still runs, so one tap does both.
- Sidebar swipe click-suppression always disarms, even when the browser never fires the drag's trailing click, so a stale flag can never eat a later tap.
- Quick taps after a sidebar swipe no longer miss their button: releasing a drag at rest snaps instead of restarting the 350ms glide, and the collapsing body stays hittable until the glide finishes instead of going dead instantly while still fading.
- Flung sheets settle with the finger's own energy (velocity-aware duration, still capped at the 350ms motion spec) instead of always racing a fixed 350ms, so buttons are back at rest sooner. Also fixed the custom settle duration being silently wiped by shorthand removal in Blink, which had pinned every release to the full 350ms.

## [1.2.2] - 2026-09-18

### Fixed
- Hidden clocks stay manageable: their sidebar row parks the visibility (eye) and delete (trash) buttons permanently, and the timezone selector expands into the remaining width. Visible rows still collapse both buttons.
- Row actions no longer stick open after the pointer leaves: reveal now matches `:focus-visible` (keyboard-only) instead of `:focus-within`, so clicking the visibility button does not hold the eye/trash strip open.

## [1.2.1] - 2026-09-17

### Fixed
- First tap after a sidebar drag toggles immediately: `suppressClick` now re-arms per gesture instead of swallowing the next caret/collapse tap (previously needed up to three taps).

## [1.2.0] - 2026-09-17

### Added
- Whole-sheet sidebar drag: swipe anywhere on the sidebar surface to expand/collapse, not just the header. Short and cancelled gestures snap back; scrollable lists keep native scrolling.

### Changed
- Mobile snackbars are now top-anchored, appearing above the sidebar sheet.
- Touch taps no longer leave buttons in a hover state; keyboard focus is unaffected.

## [1.1.0] - 2026-09-17

### Added
- Drag-to-toggle sidebar: swipe the sheet header up/down (24px threshold) to expand/collapse, with finger-tracked dragging. Short and cancelled drags snap back.

### Fixed
- Sticky touch focus/hover: tapped controls are blurred on touch-primary devices so buttons do not look stuck; keyboard focus is preserved.

## [1.0.1] - 2026-09-17

### Fixed
- Responsive sidebar and default clock layout: measure collapsed header height, correct bottom docking, animate the sheet with 350ms easing, and fit the mobile default clock to the available grid columns.

## [1.0.0] - 2026-09-16

### Added
- Grid-snapped, multi-timezone clock canvas: drag to draw clocks, move/resize on a snapping grid with adjustable cell size and top-left/center origin.
- Per-clock timezones via custom dropdowns (canvas context menu + sidebar rows).
- Clock shapes: pill or rectangle ticks with animated 160ms morph.
- Settings sidebar with reorderable clock list (pointer-driven live sorting), collapsible to a 108px header.
- Light/dark themes from Figma-generated design tokens (Tier-0 primitives -> Tier-1 semantic).
- Superellipse (squircle) corners where supported, with halved-radius fallback.

[Unreleased]: https://github.com/amirgpanah/NothingOSAnalogClock/compare/v1.2.2...HEAD
[1.2.2]: https://github.com/amirgpanah/NothingOSAnalogClock/compare/v1.2.1...v1.2.2
[1.2.1]: https://github.com/amirgpanah/NothingOSAnalogClock/compare/v1.2.0...v1.2.1
[1.2.0]: https://github.com/amirgpanah/NothingOSAnalogClock/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/amirgpanah/NothingOSAnalogClock/compare/v1.0.1...v1.1.0
[1.0.1]: https://github.com/amirgpanah/NothingOSAnalogClock/compare/v1.0.0...v1.0.1
[1.0.0]: https://github.com/amirgpanah/NothingOSAnalogClock/releases/tag/v1.0.0
