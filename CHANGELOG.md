# Changelog

## [Unreleased]

### Added
- Empty state for the Clocks section: with no clocks left, the list shows a muted "No clocks yet" prompt plus an "Add a clock" button inside a dashed, sidebar-colored superellipse zone; the button creates the default centered clock.
- Playwright empty-state regression check (`check-empty-state.mjs`, dev-only).

## [1.3.0] - 2026-09-27

### Added
- Whole-sheet drag: expand/collapse the sidebar by swiping anywhere on its surface, not just the header. Short and cancelled gestures snap back; scrollable lists keep native scrolling.
- Playwright Chromium touch regression checks (`check-touch.cjs`, dev-only).
- Hidden clocks now keep the eye and trash buttons parked in their sidebar row, so a hidden clock stays reachable and deletable; the timezone selector expands into the remaining width.
- Playwright visibility/focus regression check (`check-visibility-focus.mjs`, dev-only).
- Mouse wheel over the sidebar's non-scrollable chrome (header, short content) is direction-aware: wheel down collapses, wheel up expands; wheeling over anything scrollable inside scrolls natively and never changes state. Ignored while a pointer drag owns the gesture, and idempotent per direction, so one flick settles in one move.
- Playwright regression checks for mobile first paint, collapse fade, and wheel control (`check-mobile-collapsed.mjs`, `check-collapse-fade.mjs`, `check-wheel-toggle.mjs`, dev-only).

### Changed
- Mobile snackbars now appear at the top of the screen, above the sidebar sheet.
- Touch taps no longer leave buttons in a hover/focus state; keyboard focus is unaffected.

### Fixed
- The first tap on the collapse button after a drag now toggles immediately instead of needing three taps.
- Clicking a row's visibility button no longer leaves the eye/trash actions stuck open after the pointer leaves the row; only keyboard focus holds them open now.
- On mobile the sidebar sheet now paints collapsed on the first frame instead of starting expanded and visibly collapsing as the page opens: the state flip and header measure run in an early script, with the transition suppressed for the init flip only.
- Collapsing no longer makes the sidebar content vanish before the sheet slides down: the body's box now holds for the full 350ms glide and the content fades with it (Chrome does not interpolate `max-height: none→0`, so it used to clip at t=0 and show an empty shell moving). The box drops at rest, off-screen; expanding is unchanged.

## [1.0.0] - Initial version
