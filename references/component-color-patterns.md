# Component Color Patterns

## Two-style approach

- Subtle style:
  - Background: low-step tint
  - Foreground: high-contrast text/icon from same family
- Filled style:
  - Background: interaction step
  - Foreground: high-contrast text/icon

## Interaction states

- default: base interaction step
- hover: one darker step
- active: two darker steps
- disabled: intentionally low-contrast neutral
- focus: dedicated focus token and ring treatment

## Common mappings

- Primary button: primary filled
- Secondary button: neutral outline + primary text
- Destructive button: error filled
- Alerts/toasts: subtle style with semantic foreground
- Inputs: neutral border default, primary focus, error invalid

## Dark mode

Do not invert mechanically. Re-map semantic aliases per mode and re-run contrast checks for each state.
