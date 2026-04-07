# Safari Bug: Live Text breaks `@scope` styles on `<img>`

****UPDATE: As of 04/072026, impacts Safari 26.3 and lower, but appears to be fixed as of 26.4****
 
This repository demonstrates a Safari-specific rendering bug where **Live Text interaction overrides scoped CSS styles** applied via `@scope` on an `<img>` element.

## Summary

When Safari’s **Live Text** feature is triggered (hover or long-press on an image), it causes styles defined inside an `@scope` rule to be ignored. The browser falls back to unscoped styles, breaking layout.

## Affected Behavior

- Scoped styles:
  - `height: 100%`
  - `object-fit: cover`
- Unexpected fallback:
  - `height: auto` (from global `img` rule)

## Expected Behavior

Live Text overlays should **not interfere with CSS scoping** or cause style recalculation that ignores `@scope`.

## Actual Behavior

When Live Text activates:
- Scoped `<img>` loses `height: 100%` and `object-fit: cover`
- Global `img { height: auto }` takes over
- Layout visibly breaks

## Reproduction Steps

1. Open `index.html` in Safari
2. Ensure Live Text is enabled (default):
   - macOS: System Settings → General → Language & Region → Live Text
3. Hover over or long-press the **first image**
4. Observe layout shift

## Demo Structure

- First image: styled with `@scope` → ❌ breaks
- Second image: identical styles without `@scope` → ✅ works

## Notes

- This appears to be related to **Live Text DOM/overlay injection interfering with scoped style resolution**
- Does **not** occur when:
  - `@scope` is removed
  - Live Text is disabled

## Environment

- Safari 26.3
- macOS with Live Text enabled
