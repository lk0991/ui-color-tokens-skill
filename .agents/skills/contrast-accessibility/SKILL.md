---
name: ui-color-tokens
description: >
  Deep color system expertise for design token work. Use this skill whenever
  the user is creating a new color token set, expanding or updating existing
  color tokens, defining semantic color roles, building color scales, mapping
  WCAG contrast levels to scale steps, designing dark mode color variants, or
  making component-level color decisions. Trigger on phrases like: "create
  color tokens", "add a new color to my system", "define my semantic colors",
  "build a color scale", "what step should I use for X", "dark mode colors",
  "WCAG contrast for tokens", "color role", "status colors", or any request
  to design or review how color is structured in a design system. Also trigger
  when a user shares hex values or brand colors and wants to know how to turn
  them into a token-ready system. Use alongside the design-tokens skill for
  full DTCG output and broader token pipeline work.
---

# UI Color Token Design

A production-ready framework for designing color systems as part of a token
architecture. Covers semantic roles, scale construction, WCAG contrast mapping,
usage rules, and dark mode.

---

## Skill positioning

| This skill | design-tokens skill |
|---|---|
| Color depth: scales, roles, contrast, dark mode | Full token pipeline: color + space + type + motion + elevation |
| Deciding what your color tokens should be | Formatting and outputting DTCG JSON, Figma variable structure, AI contract |
| Auditing color decisions | Auditing the full token set |

When to use both: Use this skill to design the color layer, then hand off to
`design-tokens` for DTCG JSON output and Figma variable structure.

---

## Step 0 - Detect the task

Before doing anything, identify which path applies:

| Signal | Route |
|---|---|
| Starting from brand colors / hex values / a brief | -> [New color token set](#new) |
| Has an existing token set, wants to add a color | -> [Updating existing tokens](#update) |
| Unclear or mixed | Ask: "Are you starting from scratch, or adding to an existing system?" |

---

## Color architecture - three layers {#architecture}

Every color token system has three layers. Never skip or collapse them.

```text
Primitive  ->  Semantic  ->  Component (sparingly)
```

| Layer | What it is | Example |
|---|---|---|
| Primitive | The full scale. No UI intent. | `color.palette.red.700` |
| Semantic | A named role. Aliases a primitive. | `color.feedback.error.default` |
| Component | Component-scoped override. | `button.destructive.bg.hover` |

Rule: Consumers (components, AI, code) reference semantic tokens only.
Primitives are internal. Component tokens are only created when semantic tokens
are insufficient.

---

## Semantic color roles {#roles}

Every semantic color must have one fixed, unambiguous role. Never let a color
serve two different intents.

### Feedback / status colors

| Role | Hue | Use |
|---|---|---|
| Success | Green | Positive outcome, confirmation, completed action |
| Error | Red | Failure, invalid input, destructive outcome |
| Warning | Amber / Orange | Caution, reversible risk, attention needed |
| Info | Blue | Neutral notification, hints, non-critical messages |

### Brand / interaction colors

| Role | Use |
|---|---|
| Primary | Main CTAs, active states, key interactive elements |
| Secondary | Supporting actions, alternative paths |
| Accent | Highlights, decorative emphasis, selected states |

### Surface and text colors

| Role | Use |
|---|---|
| Background base | App/page canvas |
| Surface 1 | Cards, panels, elevated containers |
| Surface 2 | Modals, popovers, overlays |
| Text primary | Body copy, main labels |
| Text secondary | Supporting text, captions, metadata |
| Text disabled | Non-interactive, unavailable states |
| Text on-color | White/light text on colored backgrounds |
| Border default | Input outlines, card edges |
| Border focus | Keyboard focus ring (typically Primary) |

---

## Color scale structure {#scale}

Every color family needs a minimum 11-step scale. Steps encode contrast level.
If the scale is built correctly, the step number tells you the WCAG level.

```text
50    Near-white tint       Backgrounds only
100   Very light tint       Backgrounds only
200   Light tint            Decorative, no text on white
300   Medium light          Decorative, no text
400   Mid-tone              Icons, illustrations (WCAG A)
500   Base / brand value    Reference hue - do not use directly in UI
600   Slightly darker       Large text, icons on white (3:1, WCAG A)
700   AA on white           Body text minimum (4.5:1, WCAG AA)
800   Strong / dark mode    Strong emphasis, body on light surfaces
900   AAA on white          High-contrast body text (7:1, WCAG AAA)
1000  Darkest shade         Near-black, maximum contrast
```

### How to build a scale (HSB method)

Use the HSB color model to generate scale steps scientifically:

1. Set the hue and fix saturation at 100%.
2. Start at 100% brightness (step 50 / lightest).
3. Darken in 10% brightness increments.
4. Measure WCAG contrast ratio against white at each step.
5. Record the brightness value where each threshold is crossed (3:1, 4.5:1, 7:1).
6. Map those brightness values to corresponding scale steps (600, 700, 900).
7. Reduce saturation slightly if the result needs to harmonize with a brand palette.

This gives you an auditable, reproducible scale where step numbers reliably
predict contrast level.

### Hue-specific contrast behavior

Not all hues behave equally when darkened. Plan semantic role assignments
around these characteristics:

| Hue family | WCAG AA behavior | WCAG AAA behavior | Notes |
|---|---|---|---|
| Red | Stays vivid (~90% brightness) | Remains clear (~70%) | Excellent for Error |
| Blue | Outstanding, barely darkened | Nearly unchanged at AAA | Best hue for high-contrast UI |
| Violet / Purple | Appears clear and vibrant at AA | Remains bright at AAA | Reliable for Primary or Accent |
| Green | Needs heavy darkening (~50% brightness) | Very dark (~40%), loses clarity | Usable for Success; validate carefully |
| Yellow / Amber | Loses recognizability quickly; hard to reproduce in RGB | Extremely difficult | See warning note below |

Warning color (Amber/Yellow): Yellow is the most problematic hue for WCAG
compliance. It loses recognizability before reaching AA on white. If your
system uses yellow/amber for Warning:

- Shift hue toward orange (30-40 degrees) to gain contrast headroom.
- Always use the filled style for Warning; subtle style is nearly impossible to
  make accessible at this hue.
- Test with a contrast checker; do not rely solely on step position.

### Contrast quick-reference

| Step range | Contrast vs. white | WCAG level | Valid for |
|---|---|---|---|
| 1000, 900 | 7:1+ | AAA | Body text, outdoor / high ambient |
| 800, 700 | 4.5:1 | AA | Body text - minimum for product UI |
| 600 | 3:1 | A | Large text, icons, buttons |
| 50-300 | < 3:1 | Fail on white | Backgrounds only |

Contrast ratio is not full accessibility. WCAG ratios do not account for color
blindness. A red/green pair may pass contrast thresholds but still be
indistinguishable to users with deuteranopia. Always validate with a color
blindness simulator and never rely on hue alone to convey meaning. Pair color
with a text label, icon, or pattern.

### Forbidden combinations

Steps 50-300 must never appear on white as text or icon colors. They only
function as surfaces, paired with dark text from the same family.

| Background step | Minimum text step |
|---|---|
| 50 | 800 (AA) or 1000 (AAA) |
| 100 | 800 (AA) or 1000 (AAA) |
| White | 700 (AA) or 900 (AAA) |

---

## Usage rules {#usage}

### Two visual styles per semantic color

Subtle / tinted - low emphasis, informational:

- Background: `[Color]-50` or `[Color]-100`
- Text/icon: `[Color]-800` or `[Color]-900`
- Use for: inline alerts, banners, tags, badges, toasts

Filled / solid - high emphasis, actionable:

- Background: `[Color]-700` or `[Color]-800`
- Text/icon: White (`#ffffff`)
- Use for: buttons, strong alerts, status chips

### Interactive states

| State | Rule |
|---|---|
| Default | Base step (for example 700) |
| Hover | One step darker (for example 800) |
| Active / Pressed | Two steps darker (for example 900) |
| Disabled | Step 300, or Neutral 300 |
| Focus | Base color + focus ring offset (3px, 2px inset) |

### Component color reference

| Component | Token role | Style |
|---|---|---|
| Primary button | Primary 700 | Filled |
| Secondary button | Neutral border + Primary text | Outlined |
| Destructive button | Error 700 | Filled |
| Success toast | Success 100 bg + Success 800 text | Subtle |
| Error alert | Error 100 bg + Error 900 text | Subtle |
| Warning chip | Warning 700 | Filled |
| Input default | Neutral 700 border | Outlined |
| Input focus | Primary 700 border | Outlined |
| Input error | Error 700 border + Error 800 helper | Outlined |
| Link | Primary 700 | Text-only |
| Disabled | Neutral 300 bg + Neutral 400 text | Greyed |

---

## Dark mode {#darkmode}

Dark mode is not simple inversion. Recalibrate each semantic color for dark
surfaces. Scale direction flips but step numbers do not guarantee the same
contrast on dark backgrounds.

| Light mode role | Dark mode equivalent |
|---|---|
| Background (White) | Neutral 1000 or 900 |
| Surface (Neutral 50) | Neutral 800 |
| Text primary (Neutral 900) | Neutral 50 |
| Text secondary (Neutral 600) | Neutral 300 |
| Functional color (for example Green 700) | Green 300-400 (re-validate contrast) |

Always re-validate contrast ratios after inversion.

### Dark mode style variants

The two visual styles also invert in dark mode.

Subtle / tinted (dark mode):

- Background: `[Color]-900` (deep tint, not pure black)
- Text/icon: `[Color]-200` or `[Color]-300`
- Re-validate: `[Color]-200` on `[Color]-900` must still hit 4.5:1

Filled / solid (dark mode):

- Background: `[Color]-400` or `[Color]-300` (lighter than light-mode equivalent)
- Text/icon: `[Color]-1000` or Neutral 1000 (dark text on light fill)
- Re-validate: filled text on lighter fill must hit 4.5:1

The subtle style in dark mode is often under-specified. Always define both
subtle and filled variants.

---

## Workflow: New color token set {#new}

1. Gather inputs: brand hex values, existing color guidelines, and platforms
	(web, iOS, Android).
2. Assign semantic roles from the roles table and flag gaps.
3. Build primitive scales (50-1000) per family and validate contrast mapping.
4. Define semantic tokens as aliases and apply subtle + filled styles.
5. Define interactive states (hover, active, disabled, focus).
6. Define dark mode variants and re-validate all contrast ratios.
7. Hand off semantic map to `design-tokens` for DTCG JSON output and Figma
	variable structure.

---

## Workflow: Updating existing tokens {#update}

1. Identify the change: new family, new role, or existing step update.
2. Check for conflicts with existing role ownership.
3. Build/extend scale and re-validate all affected semantics.
4. Update semantic aliases and check downstream references.
5. Update dark mode mappings and re-validate dark mode contrast.
6. Deprecate safely: mark removed/renamed semantic tokens as `$deprecated`
	before deletion and communicate migration.

---

## Decision tree

```text
What does this element communicate?
|
|- A user action or navigation?
|  -> Primary or Secondary
|
|- A system state or feedback?
|  |- Positive? -> Success (Green)
|  |- Error?    -> Error (Red)
|  |- Caution?  -> Warning (Amber)
|  `- Info?     -> Info (Blue)
|
|- Structural / layout?
|  -> Neutral / Grey scale
|
`- Decorative / brand moment?
	-> Accent or Brand color

Then choose style:
|- Low emphasis?  -> Subtle (light bg + dark text)
`- High emphasis? -> Filled (dark bg + white text)

Then validate contrast:
|- Body text          -> 4.5:1 min (WCAG AA)
|- Large text / icons -> 3:1 min (WCAG A)
`- Critical / outdoor -> 7:1 min (WCAG AAA)
```

---

## Key principles

| # | Rule |
|---|---|
| 1 | One color = one meaning. Never let green serve both Success and Brand. |
| 2 | Step number = contrast level. If your scale is right, you do not need to calculate. |
| 3 | Steps 50-300 are backgrounds only. Never use as text or icon colors. |
| 4 | Stay within the same hue family. Never pair a light step of one color with a dark step of another. |
| 5 | Always define disabled states. Intentionally low contrast (~2.5:1) signals non-interactivity. |
| 6 | Dark mode is recalibration, not inversion. Always re-validate contrast after switching surfaces. |
| 7 | Test in context, not isolation. A color that works on white may fail on a Surface 2 card. |
