# Theme layer

This folder is the entire visual token system for the project, generated from
a Figma variable export (`Mode_1`, `Default`, `SDS_Light`, `SDS_Dark`, and
`Value` token JSON files). It is split into two tiers on purpose, and the two
domains (color, typography) never share a file.

```
theme/
  theme.css                     <- import this one file, nothing else
  tokens/
    color.primitives.css        Tier 0 - raw color swatches
    typography.primitives.css   Tier 0 - raw font family / scale / weight
    color.semantic.css          Tier 1 - named color roles, light + dark
    typography.semantic.css     Tier 1 - named type styles
```

## The two tiers

**Tier 0 - primitives** (`color.primitives.css`, `typography.primitives.css`)
Raw values with no assigned meaning: `--sds-color-gray-900: #1E1E1E`,
`--sds-typography-scale-03: 16px`. These never change based on light/dark
theme, and nothing outside this folder should reference them directly.

**Tier 1 - semantic** (`color.semantic.css`, `typography.semantic.css`)
Named roles that alias Tier-0 values: `--sds-color-background-default-default:
var(--sds-color-gray-900)`. This is the layer every component actually
consumes. Color semantics are theme-dependent (scoped under
`html[data-theme="light"]` / `html[data-theme="dark"]`); typography semantics
are not (a single `:root` block covers both themes, since a font's size/weight
doesn't change with light/dark).

Rule of thumb: **if a value appears in more than one place in a component
file, it's missing a semantic token; if a component file contains a raw hex or
a raw px number, something is wired to the wrong tier.**

## Switching light/dark

Nothing in this folder does the switching. Whatever JS toggles the theme just
needs to set:

```js
document.documentElement.setAttribute('data-theme', 'light'); // or 'dark'
```

`color.semantic.css` reacts to that attribute automatically. (This already
matches how the existing clock page's theme toggle works -- no JS changes
were needed to slot this in.)

## How to add a new semantic token later

1. Decide which tier it belongs to. If it's a brand-new raw value with no
   role yet, it's Tier 0 (add it to the matching `*.primitives.css`). If it's
   a name for something a component will use (e.g. "the sidebar's border
   color"), it's Tier 1.
2. Add it to the relevant `*.semantic.css` (or `*.primitives.css`) file,
   following the existing naming pattern (`--sds-color-<group>-<role>` /
   `--sds-typography-<style>-<property>`).
3. For a Tier-1 color token, define it once per theme block. Never write a
   raw hex directly in a Tier-1 file -- alias an existing Tier-0 swatch, or
   add a new Tier-0 swatch first if nothing fits.
4. Reference the new token from component CSS by name. Never reference the
   Tier-0 primitive it resolves to.

## Regenerating from Figma

These four `tokens/*.css` files were generated from the original Figma
variable JSON export, not hand-written. If new tokens are exported from
Figma again later, the same JSON -> CSS conversion should be re-run rather
than hand-editing the JSON's px/hex values into CSS by hand, since:

- Every token's exact CSS variable name is already given by the export
  itself (`$extensions."com.figma.codeSyntax".WEB`) -- that name should
  always be reused verbatim, never reinvented.
- Alias chains between tokens (e.g. a semantic token pointing at a
  primitive) are resolved by **name** (`targetVariableName`, e.g.
  `"Gray/900"`), not by the export's internal `variableId`. In this
  particular export, semantic tokens reference primitives from a separate
  published Figma library, whose IDs don't match the primitive file's own
  local IDs for the same swatch -- but the human-readable names line up
  reliably, so name-based joining is what's used.

## What is deliberately NOT in this folder

Nothing here decides where a token is *used*. No grid line, tick mark, hand,
hub, sidebar, or snackbar rule references any of these tokens yet -- that
mapping is intentionally still open and will be wired up component-by-
component once the UI for each of those is designed.
