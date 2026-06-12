---
name: design-system
description: >-
  Use when building, designing, styling, or reviewing ANY user interface - web
  (mobile-first responsive, scaling to desktop) or native iOS/iPadOS (SwiftUI).
  Enforces the shadcn_daisyui design system: the spacing grid, breakpoints and
  window size classes, navigation placement, the type ramp, color/token usage,
  shape and elevation, motion, interaction states, touch targets, and
  accessibility. Load this BEFORE writing components, screens, layouts, or
  styles, and when reviewing UI for consistency.
license: MIT
---

# shadcn_daisyui design system

Platform-portable UI guardrails for web and native iOS/iPadOS. These are the
load-bearing rules; the `references/` files hold the full detail - read the
relevant one before doing that kind of work.

## How to read these rules

- Untagged rules are universal. Rules tagged `[web]` or `[ios]` apply only to
  that platform.
- Values are dual-unit: `1rem = 16px` (web), `1pt ≈ 1px` at 1× (iOS). A value
  written `1rem / 16px / 16pt` is the same physical size everywhere.
- **HIG arbitration**: on iOS, Apple's Human Interface Guidelines win for
  navigation chrome, system gestures, and system surfaces (alerts, sheets,
  share, keyboards). These guidelines win for spacing, type roles, color
  semantics, and radius. Never invent a third option.

## Core rules (always apply)

- **Spacing** - 4px/4pt grid, blessed steps only: 4/8/12/16/24/32/48.
  Icon↔label 8px, form fields 16px apart, card interior 24px, page sections
  24-48px. No off-grid values. [web] `gap-1/2/3/4/6/8/12`.
- **Layout** - mobile-first. Window size classes: compact <640px (phones),
  medium 640-1023, expanded ≥1024. One column on compact; multi-column from
  medium/expanded. Content widths: app shell `max-w-7xl`, prose ~65ch, forms
  28-32rem. [web] gutters `px-4 sm:px-6 lg:px-8`.
- **Navigation** - compact: bottom nav, 3-5 destinations, never hidden behind a
  hamburger. expanded: sidebar (15rem) / `NavigationSplitView`. Breadcrumbs at
  medium+ only. Push = drill-down; sheet/modal = self-contained task.
- **Touch targets** - 44pt / 2.75rem minimum effective hit area on touch
  surfaces. Desktop-dense controls may be smaller; compact primary actions go
  `btn-lg` / full-width; small controls (checkboxes) are wrapped in a tappable
  label row.
- **Typography** - six roles: page title (text-3xl bold), section (text-xl
  semibold), subtitle (text-lg medium), body/prose (text-base), UI/controls
  (text-sm, the default), label (text-xs). Weights: 500 controls, 600 titles,
  700 page title only. Never bold body copy for emphasis.
- **Color** - semantic tokens only, never literal colors. One primary action per
  region; emphasis steps primary → secondary → outline → ghost. `destructive`
  only for irreversible actions, always confirmed. Status colors (info/success/
  warning/error) always mean status. Brands recolor by overriding theme tokens,
  never inline.
- **Shape & elevation** - radius by role: md (8px) fields/buttons, lg (10px)
  popovers/menus, xl (14px) cards/dialogs, full for pills. Surfaces are flat:
  borders separate, shadows are garnish (`shadow-xs` controls, `shadow-sm`
  cards/overlays - nothing more). Never hardcode radii.
- **Motion** - 150ms micro states, ~180ms small surfaces, 300ms sheets/drawers;
  ease/ease-out; animate opacity/transform only. Respect reduced motion.
- **Interaction** - full state ladder (hover is pointer-only and never
  load-bearing; focus-visible ring; disabled keeps variant color at 50%, never
  grey-washed). Async actions show progress in place and disable the control.
- **Accessibility** - contrast 4.5:1 body / 3:1 large & UI; never remove
  focus indication; every control labeled; decorative icons hidden from
  assistive tech; sentence case; buttons start with verbs; errors say what
  happened and how to fix it.

## Reference files (read on demand)

| Working on… | Read |
|---|---|
| Units, HIG arbitration, web↔SwiftUI token map | `references/foundations-platforms.md` |
| Contrast, focus, labels, reduced motion, UI writing | `references/foundations-accessibility.md` |
| Breakpoints, window classes, content widths, page scaffold | `references/foundations-layout.md` |
| Padding/margins, the grid, where each step is used | `references/foundations-spacing.md` |
| Nav placement per size class, destination limits, push vs sheet | `references/foundations-navigation.md` |
| State ladder, touch targets, dismissal | `references/foundations-interaction.md` |
| Token usage, emphasis ladder, brand splash rules | `references/styles-color.md` |
| Type ramp, weights, iconography | `references/styles-typography.md` |
| Radius roles, elevation ladder | `references/styles-shape-elevation.md` |
| Durations, easings, what not to animate | `references/styles-motion.md` |

## Platform notes

- **[web] Phoenix + shadcn_daisyui**: use the package's components and themed
  daisyUI classes; never hand-roll component markup or use raw color utilities.
  The package ships its own `usage-rules.md` (component picking, forms, theming)
  synced via `mix usage_rules.sync` - defer to it for component-level specifics.
- **[ios] SwiftUI**: build against the `ShadcnDaisyUI` Swift package's tokens
  (`Color.sd*`, `Spacing`, `Radius`, `Font.sd*`, `Motion`, `Elevation`). Never
  reference literal colors/sizes; dark variants are baked into the tokens.
