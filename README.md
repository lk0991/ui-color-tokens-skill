# ui-color-tokens-skill

A standalone Copilot skill for designing UI color token systems with strong accessibility and contrast guidance.

## Contents

- `.agents/skills/ui-color-tokens/SKILL.md`
- `references/color-architecture.md`
- `references/color-scale-playbook.md`
- `references/component-color-patterns.md`

## What this skill enforces

- Clear minimum contrast tiers (3:1, 4.5:1, 7:1)
- Semantic color discipline (one meaning per hue)
- Background-vs-foreground token boundaries
- Context-aware validation for cards, surfaces, and dark mode
- Explicit disabled-state contrast behavior

## Operating model

- SKILL file is intentionally thin and execution-focused.
- Long-form guidance lives in `references/`.
- Output is designed for handoff to a full token pipeline skill.
