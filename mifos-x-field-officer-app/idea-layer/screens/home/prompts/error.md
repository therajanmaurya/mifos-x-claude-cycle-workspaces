---
ui_yaml_sha: 4713cbb99bfa625ab87c0226c812d0245dace5264a36e234ce2aad5db0fac330
design_md_hash: c1e7dbe50f7725a08e0369f4cb0659b8c1e56ac645d128a4c90c66b8618666ef
app_shell_hash: 89077f8f960080911cf9c2b934ba619c11591fcb24da55987a5a1bb79f349739
design_read_hash: 
content_hash: fd8fadbdbc166b97df996b18a6a045336812f0ebfbca6f6ef4976929125fb721

design_read_aesthetic: taste-default
design_read_dials: {variance: 7, motion: 6, density: 4}
aesthetic_variant_override: null
archetype: error_state

feature: home
state: error
state_visibility: error

project_id: '10780096558615730514'
design_system_id: '9551377288795375599'

generated_by: stitch-prompt-build.ts v2.1.0
prompt_template_version: stitch-per-state-v3.1.0
craft_rules_version: v1.5.0
---

# home — error state

> Auto-generated from screens/home/ui.yaml @ SHA 87be5117105cd272
> Stitch DesignSystem: 9551377288795375599
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

> DO NOT invent navigation, tabs, or screens beyond the declared app-shell (Home, Clients, Centers, Groups) plus the composition below. Every nav item you render MUST come from that list.
> Only elements that navigate or perform an action may look tappable (cursor, ripple, pressed state). DO NOT add tap affordances to decorative content — page titles, section headings, avatars, standalone icons, badges, and static labels are NOT interactive.
> The concrete figures below are REALISTIC SAMPLE (demo) data, not fixed values — render believable content of the same KIND and MAGNITUDE (currency amounts, counts, percentages, names, timestamps). Exact reproduction is NOT required; realism and consistency ARE. Never use lorem, generic numbered placeholders, or empty content.
> **EXCEPTION — RENDER VERBATIM, NEVER SUBSTITUTE.** The licence above does NOT apply to any of the following, which must appear EXACTLY as declared, character for character, or be omitted entirely: emergency / crisis / helpline numbers and shortcodes (e.g. 988, 741741) and the ORGANISATION NAMES attached to them · legal, consent, privacy and medical-disclaimer text · medication names and dosages · security codes, auth codes and account identifiers. For these, a plausible substitute is a FABRICATION, not realism: inventing or renaming a crisis line sends a person in danger to something that does not answer. If such a value is absent from the declared data, render the element EMPTY and leave it visibly unresolved — never fill the gap with an invented one.
> **NO INVENTED CLAIMS OR CONTENT.** Render only what the Composition, Layout, Shell and demo data below declare. Do NOT add: rankings or superlatives ("#1", "best", "most trusted"), guarantees or percentages ("100% fit", "zero fee", "on-time guarantee"), certifications, approvals or permits, awards, testimonials or ratings, copyright lines, years or legal entity names, navigation items, footer links, sections, badges or features not listed, and product, vehicle or brand model names not given. If space remains, leave it as calm whitespace; never fill it with invented copy.

## Archetype: error_state

## Layout
- type: scrollable_column
- padding: default
- alignment: start
- responsive (RULE-MOCKUP-RESPONSIVE-001): fluid full-width layout with no fixed-width root and no phone-width max-width cap (never a bare max-w-md or fixed pixel max-width root). Compact (window under 600 wide): single column, header, then the error block, then quick actions in a 4-column grid, then Recently opened. Medium (600 to 840 wide): header spans full width; below it TWO columns: left = the error block (Couldn't load your day + Retry), right = quick actions + Recently opened (ui.yaml tablet layout: left = collections/work queue/meetings region, right = portfolio/quick actions/recent). Expanded (840 wide and up): the same two-column split inside a centred content container capped near 1200 wide (max-w-7xl) with wider gutters; quick actions may widen to one 7-across row. Use Tailwind md:/lg: breakpoints. Any phone size is a proportion reference only, never the canvas.

## Composition (top → bottom)
1. **header** (#header) — title: "Good morning, Irving", subtitle: "CENTRAL · Mon 26 Oct 2026 · Mifos field officer gateway", right_actions: [Profile, settings]
2. **error_state** (#screen_error_retry) — title: "Couldn't load your day", subtitle: "Check your connection and try again. Quick actions still work.", label: "Retry", on_click: { action: retry_all_cards }
3. **action_grid** (#quick_actions) — title: "Quick actions", items: [New client (person_add), New group (groups), New centre (domain), Collection sheet (fact_check), Run reports (bar_chart), Search (search), Path Tracker (person_pin_circle)] (render EXACTLY these, in this order — do not rename, add, or drop any)
4. **list** (#recent_card) — title: "Recently opened"

## State-specific behavior
- Error state: render ONLY the components in the composition below. It declares NO illustration — do not add one. Keep its declared Retry action.

## Content source manifest
- (no demo collections bound for this state)

## Components (vocabulary used in this prompt)
- action_grid
- error_state
- header
- list

## Shell (app-shell resolved for this state)
- Home: navigates to home
- Clients: navigates to clients
- Centers: navigates to centers
- Groups: navigates to groups
- Render MUST keep nav/bar elements consistent with the list above — present or absent, never partial.

## Tokens (design-tokens roles consumed)
- Colors: primary / secondary / surface / on-surface / on-surface-variant / error (M3 standard roles).
- Typography: body-large / title-large (M3 standard roles).
- Spacing: gap.sm / gap.md / gap.lg.
- ALL token references are by name from the uploaded design system — no hex literals, no inline size values.

## Self-Validation Checklist (MANDATORY)

Before returning the rendered mockup, verify ALL of these are true. If any fails, FIX the output and re-render.

- [ ] **Per-state shape:** the render shows ONLY this state ("error"). Do not blend multiple states into one mockup.
- [ ] **Realistic content:** every text label and data point is realistic, believable, and consistent with the ILLUSTRATIVE sample content above (this project's own domain). Figures may differ from the samples as long as they are realistic and of the same kind/magnitude — verbatim reproduction is NOT required. NO lorem, NO generic numbered placeholders, NO empty strings.
- [ ] **Token fidelity:** colors come from the uploaded design system (primary/secondary/surface/etc.) by name; spacing comes from declared scale tokens. No invented hex codes, no invented size literals.
- [ ] **Component vocabulary:** every component in the render maps to a named design-system component (Card, FAB, BottomBar, etc.) — no invented or off-system components.
- [ ] **Archetype honored:** the layout follows the "error_state" archetype skeleton — composition order top → bottom matches the Composition section.
- [ ] **App-shell parity:** if a bottom nav, top app bar, or FAB appears in the render, it matches the resolved shell from the app-shell config. Shell elements are either present-and-consistent OR absent — never partial.
- [ ] **Every affordance leads somewhere:** each button, link, tab and card that LOOKS interactive resolves to a real destination — a route in this project or a section on this page. Nothing is decorative-but-clickable, and nothing points at a page that does not exist.
- [ ] **No em-dashes:** the rendered output contains NO em-dash character. Use a colon, a comma, or a full stop instead — including inside <title>, headings, and any separator between a page name and the brand name.
- [ ] **One shape system:** corner radii come from at most THREE distinct values across the whole render. Do not mix many radii.
- [ ] **Responsive (compact/medium/expanded):** single column below 600 wide; at md: (600 to 840 wide) the declared two-column split; at lg: (840 wide and up) two columns in a centred container capped near 1200 wide. The root is fluid full-width, never capped at phone width.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 10 checkpoints pass.

↑↑↑ MOCKUP PROMPT
