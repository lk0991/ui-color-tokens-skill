# Color Scale Playbook

## Recommended step model

Use an 11-step model for each hue family:

50, 100, 200, 300, 400, 500, 600, 700, 800, 900, 1000

## Default intent mapping

- 50-300: backgrounds and tints
- 400-600: decorative accents, iconography, large text candidates
- 700-800: body text and default interaction fills (validate)
- 900-1000: high-contrast and critical readability contexts

## WCAG thresholds to validate

- 3:1 for large text and iconography
- 4.5:1 for body text
- 7:1 for critical/outdoor contexts when required

## Validation guidance

1. Validate against real surfaces, not white-only tests.
2. Re-validate all semantic aliases in dark mode.
3. For warning hues (yellow/amber), verify manually with contrast tools; these hues can lose readability quickly.

## Accessibility note

Contrast ratio alone is not enough. Validate color-blind distinguishability and pair color with text/icon/pattern where meaning matters.
