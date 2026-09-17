# Changelog

## [Unreleased]

### Added
- Whole-sheet drag: expand/collapse the sidebar by swiping anywhere on its surface, not just the header. Short and cancelled gestures snap back; scrollable lists keep native scrolling.
- Playwright Chromium touch regression checks (`check-touch.cjs`, dev-only).

### Changed
- Mobile snackbars now appear at the top of the screen, above the sidebar sheet.
- Touch taps no longer leave buttons in a hover/focus state; keyboard focus is unaffected.

### Fixed
- The first tap on the collapse button after a drag now toggles immediately instead of needing three taps.

## [1.0.0] - Initial version
