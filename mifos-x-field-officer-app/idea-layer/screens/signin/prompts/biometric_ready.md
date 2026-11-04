---
ui_yaml_sha: fac06dd862aab96c9db367de11d23efbd1579d966eec71e003e537333444b29b
design_md_hash: c1e7dbe50f7725a08e0369f4cb0659b8c1e56ac645d128a4c90c66b8618666ef
app_shell_hash: 89077f8f960080911cf9c2b934ba619c11591fcb24da55987a5a1bb79f349739
design_read_hash: 
content_hash: ca95575de84561996c125120626e0e817d6024f443c63fed0550a5772e5c268a

design_read_aesthetic: taste-default
design_read_dials: {variance: 7, motion: 6, density: 4}
aesthetic_variant_override: null
archetype: form

feature: signin
state: biometric_ready
state_visibility: biometric_ready

project_id: '10780096558615730514'
design_system_id: '9551377288795375599'

generated_by: stitch-prompt-build.ts v2.1.0
prompt_template_version: stitch-per-state-v3.1.0
craft_rules_version: v1.5.0
---

# signin — biometric_ready state

> Auto-generated from screens/signin/ui.yaml @ SHA ae9c119be2f52179
> Stitch DesignSystem: 9551377288795375599
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

> This app has NO navigation chrome: no bottom navigation bar, no top app bar, no tabs, no drawer, no FAB. DO NOT invent any. Render ONLY the composition below on a single full-bleed surface.
> Only elements that navigate or perform an action may look tappable (cursor, ripple, pressed state). DO NOT add tap affordances to decorative content — page titles, section headings, avatars, standalone icons, badges, and static labels are NOT interactive.
> The concrete figures below are REALISTIC SAMPLE (demo) data, not fixed values — render believable content of the same KIND and MAGNITUDE (currency amounts, counts, percentages, names, timestamps). Exact reproduction is NOT required; realism and consistency ARE. Never use lorem, generic numbered placeholders, or empty content.
> **EXCEPTION — RENDER VERBATIM, NEVER SUBSTITUTE.** The licence above does NOT apply to any of the following, which must appear EXACTLY as declared, character for character, or be omitted entirely: emergency / crisis / helpline numbers and shortcodes (e.g. 988, 741741) and the ORGANISATION NAMES attached to them · legal, consent, privacy and medical-disclaimer text · medication names and dosages · security codes, auth codes and account identifiers. For these, a plausible substitute is a FABRICATION, not realism: inventing or renaming a crisis line sends a person in danger to something that does not answer. If such a value is absent from the declared data, render the element EMPTY and leave it visibly unresolved — never fill the gap with an invented one.
> **NO INVENTED CLAIMS OR CONTENT.** Render only what the Composition, Layout, Shell and demo data below declare. Do NOT add: rankings or superlatives ("#1", "best", "most trusted"), guarantees or percentages ("100% fit", "zero fee", "on-time guarantee"), certifications, approvals or permits, awards, testimonials or ratings, copyright lines, years or legal entity names, navigation items, footer links, sections, badges or features not listed, and product, vehicle or brand model names not given. If space remains, leave it as calm whitespace; never fill it with invented copy.

## Archetype: form

## Visual treatment (THIS SCREEN'S OWN brief — overrides the form archetype default; honor this hierarchy)
- A calm, confident CREDENTIAL screen for a field worker: generous vertical rhythm, one clear primary action, nothing competing with it. This is the first screen of a banking tool — it should read as trustworthy and quiet, not playful.
- Vertical order: a small instance chip at the very top, then the brand mark, then a two-line title, then the two fields, then the primary submit, then the biometric accelerator when present. A short legal consent line sits pinned at the bottom.
- The INSTANCE CHIP is the signature element and must not look like a button: a compact, low-contrast pill with a small server glyph showing host and tenant, with a subtle chevron implying it can be changed. It is information first and an affordance second.
- CLOSED SET — render EXACTLY the components listed in the Composition and NOTHING ELSE. Every element here maps to shipped code; an extra affordance is a claim this product does not support.
- DO NOT add: 'remember me', 'forgot password', 'create account'/'sign up', social or SSO buttons, a QR scanner, an offline-cache banner, an officer/employee ID field, a language picker, or a version footer. None of these exist.
- NO TOP APP BAR and no chrome above the instance chip: no gear, no overflow, no back arrow. This is the unauthenticated gate — there is nowhere to go back to.

## Layout
- type: scrollable_column
- padding: default
- alignment: start
- responsive: fluid full-width, no phone-width root cap; Tailwind md:/lg:. Compact (<600 wide): full-width form. Medium (600-840 wide): centred card max ~480 wide on a brand-tinted ground. Expanded (>=840 wide): two panes, brand panel left (Mifos X mark + product line), sign-in card right, max ~1200 wide.

## Composition (top → bottom)
1. **assist_chip** (#instance_chip) — label: "apis.mifos.community · mifos-bank-1", on_click: { action: navigate, target: serverconfig }
2. **image** (#logo) — Mifos X mark (four triangles around a white X), never a bank icon
3. **text_block** (#title)
4. **text_button** (#biometric_action) — renders_states: ["biometric_ready"] (render EXACTLY these 1, in this order — do not rename, reword, add or drop any), on_click: { action: submit, target: authenticatebiometric }
5. **outlined_text_field** (#username_field)
6. **outlined_text_field** (#password_field)
7. **button** (#login_button) — disabled_when: ["submitting", "locked_out"] (render EXACTLY these 2, in this order — do not rename, reword, add or drop any), on_click: { action: submit, target: authenticate }
8. **legal_text** (#consent_text)

## State-specific behavior
- Custom state "Biometric Ready" — render per the composition below.

## Content source manifest
- (no demo collections bound for this state)

## Components (vocabulary used in this prompt)
- assist_chip
- button
- image
- legal_text
- outlined_text_field
- text_block
- text_button

## Shell (app-shell resolved for this state)
- This app declares NO bottom navigation, NO top app bar, NO tabs and NO drawer.
- The screen is a single full-bleed surface. Render NO app chrome whatsoever.

## Tokens (design-tokens roles consumed)
- Colors: primary / secondary / surface / on-surface / on-surface-variant / error (M3 standard roles).
- Typography: body-large / title-large (M3 standard roles).
- Spacing: gap.sm / gap.md / gap.lg.
- ALL token references are by name from the uploaded design system — no hex literals, no inline size values.

## Self-Validation Checklist (MANDATORY)

Before returning the rendered mockup, verify ALL of these are true. If any fails, FIX the output and re-render.

- [ ] **Per-state shape:** render ONLY the "biometric_ready" state. Do not blend states.
- [ ] **Realistic content:** every label and figure realistic and of the same kind and magnitude as the samples; exact values may differ. No lorem, no numbered placeholders, no empty strings.
- [ ] **Token fidelity:** colors and spacing by design-system name. No invented hex, no invented size literals.
- [ ] **Component vocabulary:** every component maps to a named design-system component. Nothing off-system.
- [ ] **Archetype honored:** layout follows the "form" skeleton; composition order top to bottom.
- [ ] **App-shell parity:** nav / app bar / FAB match the resolved shell exactly, or are absent. Never partial.
- [ ] **Every affordance leads somewhere:** anything that looks interactive resolves to a real destination. Nothing decorative-but-clickable.
- [ ] **No em-dashes:** zero em-dash characters anywhere, <title> included. Use a colon, comma or full stop.
- [ ] **One shape system:** at most THREE distinct corner radii.
- [ ] **Responsive:** compact single column, medium centred card, expanded two-pane, via md:/lg: breakpoints; no phone-width root cap.

If any of these fail and the fix isn't clear → halt rendering and surface "Self-validation failed at: {checkpoint}."

Return ONLY when all 10 checkpoints pass.

↑↑↑ MOCKUP PROMPT
