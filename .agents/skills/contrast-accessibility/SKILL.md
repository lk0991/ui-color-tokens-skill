---
name: contrast-accessibility
description: Enforce practical contrast decisions for interfaces, with strict thresholds for outdoor and critical UI.
---

# Contrast Accessibility

Use this skill when defining or reviewing color systems for readability, accessibility, and environment-aware reliability.

## Minimum contrast targets

- Body text and icons: 4.5:1 min (WCAG AA)
- Large text and icons: 3:1 min (WCAG A)
- Critical and outdoor UI: 7:1 min (WCAG AAA)

## Key principles

| # | Rule |
|---|---|
| 1 | One color = one meaning. Never let green serve both Success and Brand. |
| 2 | Step number = contrast level. If your scale is right, you do not need to calculate every pairing. |
| 3 | Steps 50–300 are backgrounds only. Never use them as text or icon colors. |
| 4 | Stay within the same hue family. Never pair a light step of one color with a dark step of another. |
| 5 | Always define disabled states. Intentionally low contrast (~2.5:1) signals non-interactivity. |
| 6 | Dark mode is recalibration, not inversion. Always re-validate contrast after switching surfaces. |
| 7 | Test in context, not isolation. A color that works on white may fail on a Surface 2 card. |

## Workflow

1. Assign semantic roles first: Primary, Success, Warning, Danger, Neutral.
2. Map each role to one hue family only.
3. Pick step pairs from the same family that satisfy the target contrast tier.
4. Validate contrast on real surfaces (page background, cards, overlays, dark mode).
5. Define disabled tokens intentionally and keep them visibly non-interactive.

## Output format

When reviewing a palette, return:

1. Pass/fail by tier: 3:1, 4.5:1, and 7:1.
2. Violations grouped by semantic role.
3. Exact replacement token pairs that fix each violation.
4. A short risk note for outdoor use and dark mode.
