---
ui_yaml_sha: caca124ad22d8a7ad5a294b9446fbff54ffe7a78e7feafe414b9cb8932d96bca
design_md_hash: c1e7dbe50f7725a08e0369f4cb0659b8c1e56ac645d128a4c90c66b8618666ef
app_shell_hash: 89077f8f960080911cf9c2b934ba619c11591fcb24da55987a5a1bb79f349739
design_read_hash: 
content_hash: 294105dd6c25c58589a74869c0b4bd3dd42d5efe263b6b0b32481d3d4bf5274b

design_read_aesthetic: taste-default
design_read_dials: {variance: 7, motion: 6, density: 4}
aesthetic_variant_override: null
archetype: empty_state

feature: offlineSync
state: empty
state_visibility: empty

project_id: '10780096558615730514'
design_system_id: '9551377288795375599'

generated_by: stitch-prompt-build.ts v2.1.0
prompt_template_version: stitch-per-state-v3.1.0
craft_rules_version: v1.5.0
polished_by: claude-in-session (Step 2 POLISH, source = screens/offlineSync/ui.yaml + preview/empty.html; responsive mandate RULE-MOCKUP-RESPONSIVE-001)
---

# offlineSync — empty state

> Polished from screens/offlineSync/ui.yaml @ SHA e3121448596a0a6e + the approved preview tier.
> Stitch DesignSystem: 9551377288795375599

↓↓↓ MOCKUP PROMPT

Design the empty state of the Offline sync screen for **Mifos X Field Officer**, a microfinance field-officer app that keeps centres, groups and clients on the device so the officer can work where there is no signal. Material 3 light theme, responsive layout (phone is the compact reference, not the canvas), the design system's own type scale (do not change the font). Responsive: fluid full-width layout with no fixed-width root and no phone-width max-width cap; use Tailwind md:/lg: breakpoints. Compact (<600dp): one column in the order Summary, Empty, Sync, cards full width minus 16dp insets. Medium (600-840dp): two-column list-detail, a left column about 360dp wide stacking Summary and Sync, and a right column filling the rest with the Empty card, its content centred in the column, 24dp gutters. Expanded (>=840dp): the same two columns centred in a content area capped near 1200dp, left column 400dp, the empty card body text capped near 480dp wide so it never stretches into long lines.

Palette: background #FAFAFB, surface #FFFFFF, onSurface #0F172A, onSurfaceVariant #475569, primary #4338CA, onPrimary #FFFFFF, primaryContainer #E0E7FF, onPrimaryContainer #1F1D75, secondary #059669, secondaryContainer #D1FAE5, outline #94A3B8, outlineVariant #CBD5E1.

Shell: this is a Settings sub-screen. Top app bar with a back arrow and the title only, spanning the full window width. NO bottom navigation bar, NO drawer, NO FAB in this state (the primary action lives in the empty card).

**Component 1 - Top App Bar** (64dp tall, background #FAFAFB): back arrow, title "Offline sync" semibold title-large #0F172A.

**Component 2 - Summary Card** (16dp radius, white, 1dp #CBD5E1 border, 16dp padding): one chip "Online" (#D1FAE5 with a dot). Three level tiles with dashed #CBD5E1 borders, each showing "0" in #94A3B8 above "Centres", "Groups", "Clients" with icons. Caption "Not synced yet, Manual".

**Component 3 - Empty Card** (same card style, centered content, 24dp padding, list_screen archetype in its empty form): a small hierarchy motif of three 44dp rounded-square icon tiles joined by short #CBD5E1 connectors: groups icon on #E0E7FF, three-people icon on #F3E8FF, person icon on #D1FAE5. Title "Nothing on this device yet" semibold. Body in #475569, at most 3 lines: "Choose the centres, groups or clients you'll visit and sync them before you head out. Everything under them opens here without signal." A 48dp pill button "Add records" filled #4338CA with a plus icon.

**Component 4 - Sync Card** (same card style): heading "Sync", segmented control "Manual" selected and "Automatic", info line "Syncing downloads a lot of data. Only the records you choose come to this device."

DO NOT add illustrations, stock imagery or marketing copy beyond the icon motif. DO NOT show uploads, payloads or queues. DO NOT render a bottom navigation bar or a FAB. DO NOT use em-dash characters anywhere.

Inviting and clear: lots of calm white space, one indigo #4338CA call to action, and the centre to group to client motif quietly explains what gets downloaded.

↑↑↑ MOCKUP PROMPT
