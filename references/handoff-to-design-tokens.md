# Handoff Example: ui-color-tokens -> design-tokens

Use this example to pass a completed color decision package into the design-tokens skill.

## Input context (from ui-color-tokens)

- Route used: `new`
- Modes: `light`, `dark`
- Platforms: `web`, `iOS`

### Semantic role map

- `color.text.primary` -> neutral role
- `color.text.secondary` -> neutral supporting role
- `color.bg.base` -> neutral base surface
- `color.bg.surface` -> neutral elevated surface
- `color.feedback.success.default` -> success role
- `color.feedback.warning.default` -> warning role
- `color.feedback.error.default` -> error role
- `color.feedback.info.default` -> info role
- `color.border.default` -> neutral border
- `color.border.focus` -> primary focus ring

### Primitive step guidance

- Neutrals: text defaults target 700/900 in light mode, 50/300 in dark mode.
- Primary: interaction defaults target 700 with hover 800 and active 900 in light mode.
- Feedback colors: subtle uses low-step backgrounds + high-step text; filled uses 700/800 backgrounds with high-contrast foregrounds.

### Contrast targets

- Body text: >= 4.5:1
- Large text/icons: >= 3:1
- Critical contexts: >= 7:1 where required

## Handoff package

Provide the following to design-tokens:

1. Final semantic token map
2. Mode mappings (light/dark)
3. Contrast constraints by role
4. Deprecation notes (if replacing old role names)
5. Instruction: "Generate DTCG JSON and TOKEN_CONTRACT.md"

## Example handoff message

"Generate full DTCG outputs from this semantic map. Keep semantic paths stable across light/dark modes, emit primitive/semantic layers, include descriptions for all semantic/component tokens, and produce TOKEN_CONTRACT.md using the repository contract template."
