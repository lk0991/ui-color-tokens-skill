# Color Architecture Reference

Use this reference for detailed decisions while running the ui-color-tokens skill.

## Three-layer model

Primitive -> Semantic -> Component (sparingly)

- Primitive: raw scales only, no UI intent in token names.
- Semantic: intent-driven aliases; primary consumer interface.
- Component: component-specific escape hatch only when semantic tokens are insufficient.

## Role model

Recommended semantic roles:

- Interaction: primary, secondary, accent
- Feedback: success, warning, error, info
- Surfaces: bg.base, bg.surface.1, bg.surface.2
- Text: text.primary, text.secondary, text.disabled, text.onColor
- Borders: border.default, border.focus

## Constraints

1. One role, one meaning.
2. Avoid using primitive tokens directly in component code.
3. Add component tokens only after semantic options are exhausted.
