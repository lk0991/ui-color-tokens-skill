---
name: ui-color-tokens
description: Design and audit the color layer of a token system, then hand off to design-tokens for full DTCG output.
---

# UI Color Tokens

This skill is for deciding color semantics, scales, contrast thresholds, and
light/dark mappings. It does not own full token pipeline output.

For full JSON, Figma variable structure, and token governance artifacts, hand
off to `design-tokens` after this skill completes.

## Preflight

Before proposing changes:

1. Read existing token files and docs in the repo.
2. Reuse existing naming and role conventions unless the user asks for a reset.
3. If project docs exist, align vocabulary to them.

## Execution contract

Always do these steps in order:

1. Detect route (`new`, `update`, or `audit`).
2. Ask at most one clarifying question if required inputs are missing.
3. Produce the route outputs exactly as listed below.
4. End with handoff instructions for `design-tokens`.

## Route detection

- `new`: starting from brand colors, hex values, or a brief.
- `update`: existing token system, adding or changing color behavior.
- `audit`: user provides a color token set and asks for critique.
- If unclear, ask one question: "Are you starting from scratch, updating an
  existing system, or asking for an audit?"

## Global rules

Apply these on every route:

1. Use three layers: `Primitive -> Semantic -> Component (sparingly)`.
2. Semantic tokens are the primary consumer interface.
3. One color role has one meaning. Avoid role overlap.
4. Validate contrast for body text (4.5:1), large/icon (3:1), and critical
   contexts (7:1 where applicable).
5. Dark mode requires re-validation; do not invert blindly.

Reference details:

- `references/color-architecture.md`
- `references/color-scale-playbook.md`
- `references/component-color-patterns.md`

## Route: new

Use when creating a color system from scratch.

### Required inputs

- Brand colors or palette seed values
- Target themes/modes (light only or light+dark)
- Target platforms (web, mobile, both)

### Outputs

Return all of these:

1. Semantic role map
: primary, secondary, accent, success, warning, error, info, neutrals
2. Primitive scale plan per family
: 50-1000 with target role usage guidance
3. Contrast mapping table
: which steps satisfy 3:1, 4.5:1, 7:1 on key surfaces
4. Light and dark semantic mapping
: role -> primitive alias by mode
5. Risk notes
: hue-specific risks and where manual checker verification is mandatory

## Route: update

Use when expanding or changing an existing system.

### Required inputs

- Existing color tokens (or representative subset)
- Requested change (new hue, role reassignment, or step changes)

### Outputs

Return all of these:

1. Change impact summary
: what semantic roles and components are affected
2. Conflict checks
: role collisions, contrast regressions, dark-mode mismatches
3. Updated role/step recommendations
: old -> new aliases with rationale
4. Migration notes
: deprecations and safe replacement guidance

## Route: audit

Use when reviewing an existing color token set.

### Outputs

Return all of these:

1. Findings table
: severity, token/group, issue, recommendation
2. Coverage gaps
: missing roles, missing states, missing dark mode pairings
3. Contrast risk list
: failing or likely-failing combinations by context
4. Prioritized fix order
: high-leverage sequence to remediate

## Handoff to design-tokens

After any route, end with a short handoff package that `design-tokens` can
execute without interpretation:

1. Final semantic token map
2. Mode mappings (light/dark)
3. Deprecation/migration notes (if any)
4. Explicit instruction: "Generate DTCG JSON and TOKEN_CONTRACT.md"

## Stop conditions

Stop and ask for user input only when:

1. No starting palette or existing tokens are available.
2. The role map is contradictory and cannot be resolved by one default rule.
3. The user requests WCAG claims without any target surface context.
