---
name: "designer-playbook"
description: "Designer specialty playbook — DESIGN.md update procedure and brand-asset handoff format for the Packlinx product surface. Read before changing the design system or shipping new visual assets."
slug: "designer-playbook"
metadata:
  paperclip:
    slug: "designer-playbook"
    skillKey: "local/5ee412747b/designer-playbook"
  paperclipSkillKey: "local/5ee412747b/designer-playbook"
  skillKey: "local/5ee412747b/designer-playbook"
key: "local/5ee412747b/designer-playbook"
---

# Designer Playbook

Specialty bundle for the Packlinx Designer role. Covers two recurring
artifacts: DESIGN.md updates (the canonical design-system source of truth)
and brand-asset handoff to engineering.

Common skills handle voice, decision protocol, and company context. Do not
duplicate that content here.

## When to invoke this skill

- Adding or modifying a design token (color, type, spacing, radius)
- Adding a new component to the design system
- Handing off brand assets (logo, illustration, hero imagery) to
  engineering
- Reviewing a teammate's design or design-PR
- Writing or updating component documentation

## First principle

**Korean B2B is conservative; trust signals beat flashy UX.** Optimize the
data model, search quality, and content density before adding visual
ornament. The design system exists to remove decisions, not to add
expression.

## Part 1 — DESIGN.md update procedure

`DESIGN.md` is the canonical design-system source of truth. The runtime
loads it; engineers reference it; agents read it. Drift between DESIGN.md
and shipped CSS is a bug.

### Where it lives

`DESIGN.md` at the repo root (or `/docs/DESIGN.md`, whichever the project
uses — confirm before editing). All design tokens, component specs, and
voice rules live there. This skill is meta-procedure; the content lives
in DESIGN.md.

### When to update

Update DESIGN.md **before** the corresponding code change ships, not
after. The order is:

1. Decide the design change.
2. Update DESIGN.md with the new spec.
3. Get review (CTO sign-off for tokens; HoP sign-off for component
   patterns).
4. Implement in code, referencing the updated section.
5. Verify visual diff matches the spec.

Updating DESIGN.md after the code shipped is "documenting the past" — it's
useful but it's not the system. Reverse the order.

### What goes in each section

- **Tokens** — primitive values: color hex, type scale, spacing scale,
  radius, shadow. Tokens are the contract; components reference tokens by
  name, never raw values.
- **Components** — for each component: purpose, anatomy, states (default,
  hover, active, disabled, loading, error), accessibility notes, do/don't
  examples.
- **Patterns** — repeated combinations of components: card layouts, form
  layouts, empty states.
- **Voice** — short pointer to `packlinx-comms` for full voice rules; this
  section names visual treatments of voice (e.g., how error tone shows up
  visually).
- **Rationale** — for non-obvious choices, a one-paragraph why. Future
  designers will ask; answer once, in writing.

### Update template

```md
## <Component / Token name>

**Status:** stable | beta | deprecated
**Last changed:** <YYYY-MM-DD> by <who>
**Used in:** <list of pages or components that consume this>

### Purpose

One sentence. What problem does this solve? Why does it exist?

### Anatomy

<diagram or labeled markup>

### States

- Default
- Hover
- Active / pressed
- Focus (keyboard)
- Disabled
- Loading
- Error

### Tokens consumed

- Color: `--color-...`
- Spacing: `--space-...`
- Type: `--type-...`

### Accessibility

- Keyboard: <interactions>
- Screen reader: <semantic role, aria notes>
- Contrast: <verified ratio at smallest text size>

### Do

- Concrete usage example.

### Don't

- Concrete misuse with reason.

### Rationale (only when non-obvious)

Why this shape, why these tokens, why this constraint.
```

### Token-change rules

- **Color tokens** require contrast verification at every text size that
  uses them. WCAG AA minimum.
- **Type tokens** require Korean rendering check at all sizes (한글 has
  different visual rhythm than Latin; line-height that works for English
  often crowds Korean).
- **Renaming a token** is a breaking change — coordinate with engineering
  to update consumers in the same release.
- **Deprecating** a token: mark `deprecated` in DESIGN.md, list the
  replacement, give consumers a 30-day window before removal.

### Review and commit hygiene

- DESIGN.md changes go through the same PR process as code.
- Visual diff (Figma frame or screenshot) attached to the PR.
- Commit message mentions the affected component/token name so it's
  greppable.
- After merge, post a one-line update in the team channel: "DESIGN.md:
  added <X>; consumers should reference <token>."

### Anti-patterns

- Changing a token value without updating DESIGN.md.
- Adding a one-off color in a component file. If it's worth using, it's
  a token.
- "Temporary" component variants that never get deleted.
- Documenting visual decisions in code comments instead of DESIGN.md.
  Code comments don't get found.

## Part 2 — Brand-asset handoff format

A brand-asset handoff that doesn't follow this format costs an engineer
2–4 extra hours and ships at the wrong size or wrong format. The cost
compounds across every page that uses the asset.

### When this applies

- New logo variant
- New hero or illustration
- New iconography
- Vendor or partner brand asset (always require their handoff in this
  format too — no exceptions)

### Required deliverables (every handoff)

A handoff is incomplete unless **all** of these exist:

- [ ] **Source file** (`.fig` link or `.svg` master). The source is
      authoritative; everything else is exported from it.
- [ ] **SVG export** for every vector asset. Cleaned (no clip paths
      where unnecessary, no embedded raster, no inline styles).
- [ ] **PNG fallbacks** at 1×, 2×, 3× for raster needs. ASCII filenames.
- [ ] **WebP / AVIF** for hero imagery (engineering will optimize, but
      the source export should be lossless or near-lossless).
- [ ] **License file or note** — own asset, licensed (attach license),
      or vendor-provided (attach permission email).
- [ ] **Spec sheet** — see template below.

### Spec sheet template

```md
# Asset — <Name>

**Type:** logo | illustration | icon | hero | photo
**Source:** <Figma link or path to master file>
**License:** own | licensed (<source + terms>) | vendor-provided
            (<email link>)
**Last updated:** <YYYY-MM-DD>

## Variants

| Variant | File | Use case |
| --- | --- | --- |
| Primary | `name-primary.svg` | Default surfaces |
| Mono dark | `name-mono-dark.svg` | Dark backgrounds, single color |
| Mono light | `name-mono-light.svg` | Light single-color contexts |

## Sizing

- Min display size: <px or em>
- Recommended display size: <px or em>
- Clear space: <px multiple of asset edge>

## Color

- On-brand color tokens: `--color-...` (reference DESIGN.md tokens)
- On-vendor backgrounds: <hex values + contrast note>

## Filename rules

- ASCII only, kebab-case
- Pattern: `<asset>-<variant>-<size>.<ext>`
- No Korean characters in filenames; some CDN paths break

## Korean alt text (when this asset renders user-facing)

```
<provided Korean alt text>
```

## Engineering notes

- Required SVG attributes: `viewBox`, `xmlns`, `role="img"`, `aria-label`
- For animated assets: provide CSS-only animation spec, no JS
  dependencies
- For vendor logos: never modify the vendor's logo without written
  permission

## Out of scope

- This handoff does not cover <X>. Open a separate ticket if needed.
```

### Vendor brand-asset rules

When onboarding a vendor (per `coo-playbook` Step 2):

- Vendor must provide their logo in the format above OR Packlinx
  redraws it as part of onboarding (with vendor written approval).
- Never auto-trace a low-resolution vendor logo and ship it; it looks
  amateur and the vendor can object.
- License: vendor must explicitly grant Packlinx the right to display
  their logo on Packlinx surfaces. The COO records this; design relies
  on it.

### Anti-patterns

- Handing off a Figma link with no exports. "I'll export later" never
  happens.
- Filenames with Korean characters or spaces.
- Embedding raster images inside SVGs (defeats vector benefit).
- Shipping an asset before the spec sheet is written.
- Modifying a vendor logo (color, proportion, decoration) without
  written permission.

## Refusals

- Refuse to ship a design change without a DESIGN.md update.
- Refuse to introduce a one-off color or font that isn't tokenized.
- Refuse to override accessibility minimums for visual preference.
- Refuse to use a vendor's brand asset without their written permission.
- Refuse to ship "temporary" assets without a kill criterion in the
  ticket.

## Self-check before handoff or DESIGN.md merge

- [ ] Is DESIGN.md updated *before* the code change?
- [ ] Have I verified Korean rendering at every type size that changed?
- [ ] Is contrast verified at every text size that uses this color?
- [ ] Are filenames ASCII-only, kebab-case, with explicit variants?
- [ ] If a vendor asset, is the license / permission attached?
- [ ] Could a developer pick this up tomorrow without asking me a
      follow-up question?
