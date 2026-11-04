---
ui_yaml_sha: 4713cbb99bfa625ab87c0226c812d0245dace5264a36e234ce2aad5db0fac330
design_md_hash: c1e7dbe50f7725a08e0369f4cb0659b8c1e56ac645d128a4c90c66b8618666ef
app_shell_hash: 89077f8f960080911cf9c2b934ba619c11591fcb24da55987a5a1bb79f349739
design_read_hash: 
content_hash: dbf0a93133ce0f34928daadd10a30efecb9124639edd70df94de239afa8094f0

design_read_aesthetic: taste-default
design_read_dials: {variance: 7, motion: 6, density: 4}
aesthetic_variant_override: null
archetype: dashboard

feature: home
state: offline
state_visibility: offline

project_id: '10780096558615730514'
design_system_id: '9551377288795375599'

generated_by: stitch-prompt-build.ts v2.1.0
prompt_template_version: stitch-per-state-v3.1.0
craft_rules_version: v1.5.0
---

# home — offline state

> Auto-generated from screens/home/ui.yaml @ SHA b7d462b0f3be17c9
> Stitch DesignSystem: 9551377288795375599
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.
> Composition split across section files (Stitch composes them by name).

## Archetype: dashboard

## Layout
- type: scrollable_column
- padding: default
- alignment: start
- responsive: the primary HERO card spans FULL WIDTH; the secondary KPI/stat cards form a COMPACT 2-COLUMN GRID (2×2 for four cards) that is INTENDED and RETAINED at phone width — this dense KPI grid IS the professional dashboard layout, so do NOT collapse the stat cards to a single column. Only genuine list/activity regions remain single-column.
- breakpoints (RULE-MOCKUP-RESPONSIVE-001): fluid full-width layout with no fixed-width root and no phone-width max-width cap (never a bare max-w-md or fixed pixel max-width root). Compact (window under 600 wide): a single column in order collections, work queue, meetings, portfolio (2-column tile grid), quick actions (4-column grid), recent (render only the components the composition lists). Medium (600 to 840 wide): header spans full width; below it TWO columns: left = collections, work queue, meetings; right = portfolio, quick actions, recent (ui.yaml tablet layout). Expanded (840 wide and up): the same two-column split inside a centred content container capped near 1200 wide (max-w-7xl) with wider gutters. Use Tailwind md:/lg: breakpoints. Any phone size is a proportion reference only, never the canvas.
- grid-fit: a stat card whose value is a LONG amount (large currency figure like a full monetary total) MUST span the FULL grid width (both columns) so the figure never truncates, wraps awkwardly, or overflows its cell; compact KPIs (counts, short percentages, small integers) sit two-per-row. Keep every numeric value and its trailing badge fully inside its card — nothing may spill past the card edge.

## State-specific behavior
- Error state: render ONLY the components in the composition below. It declares NO illustration — do not add one. It declares NO Retry action — do not add a Retry button or any action the composition does not list.

## Composition (top → bottom) — split into 2 sections
1. **section-1** — see screens/home/prompts/offline.section-1.md
2. **section-2** — see screens/home/prompts/offline.section-2.md

## Content source manifest
- (none)

## Tokens (design-tokens roles consumed)
- Colors: primary / secondary / surface / on-surface / on-surface-variant / error (M3 standard roles).
- Typography: body-large / title-large (M3 standard roles).
- Spacing: gap.sm / gap.md / gap.lg.
- ALL token references are by name from the uploaded design system — no hex literals, no inline size values.

## Self-Validation Checklist
- [ ] **Responsive, phone-first (RULE-MOCKUP-RESPONSIVE-001):** design the compact phone layout first, then widen it — Tailwind md: (medium) turns it into two columns or list-detail as the screen spec's tablet layout describes, lg: (expanded) caps content width and adds columns. No fixed-width root and no phone-width max-w cap; a single stacked column at every width is a fail.
