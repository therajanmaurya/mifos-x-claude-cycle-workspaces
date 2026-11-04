---
ui_yaml_sha: caca124ad22d8a7ad5a294b9446fbff54ffe7a78e7feafe414b9cb8932d96bca
design_md_hash: c1e7dbe50f7725a08e0369f4cb0659b8c1e56ac645d128a4c90c66b8618666ef
app_shell_hash: 89077f8f960080911cf9c2b934ba619c11591fcb24da55987a5a1bb79f349739
design_read_hash: 
content_hash: 1a5b609c637992432e4ee724aedd7f9df43f047a8e09c3dba4a4c582c31564f4

design_read_aesthetic: taste-default
design_read_dials: {variance: 7, motion: 6, density: 4}
aesthetic_variant_override: null
archetype: list_screen

feature: offlineSync
state: offline
state_visibility: offline

project_id: '10780096558615730514'
design_system_id: '9551377288795375599'

generated_by: stitch-prompt-build.ts v2.1.0
prompt_template_version: stitch-per-state-v3.1.0
craft_rules_version: v1.5.0
polished_by: claude-in-session (Step 2 POLISH, source = screens/offlineSync/ui.yaml + preview/offline.html; responsive mandate RULE-MOCKUP-RESPONSIVE-001)
---

# offlineSync — offline state

> Polished from screens/offlineSync/ui.yaml @ SHA 407df55cf67e43fe + the approved preview tier.
> Stitch DesignSystem: 9551377288795375599

↓↓↓ MOCKUP PROMPT

Design the offline state of the Offline sync screen for **Mifos X Field Officer**, a microfinance field-officer app that keeps centres, groups and clients on the device so the officer can work where there is no signal. Material 3 light theme, responsive layout (phone is the compact reference, not the canvas), the design system's own type scale (do not change the font). Responsive: fluid full-width layout with no fixed-width root and no phone-width max-width cap; use Tailwind md:/lg: breakpoints. Compact (<600dp): one column in the order Offline Banner, Summary, On this device, Drafts Note, cards full width minus 16dp insets. Medium (600-840dp): the Offline Banner spans the full content width on top, then two-column list-detail: a left column about 360dp wide stacking Summary and Drafts Note, and a right column filling the rest with the On this device card and its search field, 24dp gutters. Expanded (>=840dp): the same layout centred in a content area capped near 1200dp, left column 400dp, client rows wider with the status line on the same row as the name.

Palette: background #FAFAFB, surface #FFFFFF, onSurface #0F172A, onSurfaceVariant #475569, primary #4338CA, primaryContainer #E0E7FF, secondary #059669, secondaryContainer #D1FAE5, tertiary #D97706, tertiaryContainer #FEF3C7, onTertiaryContainer #78350F, outline #94A3B8, outlineVariant #CBD5E1.

Shell: this is a Settings sub-screen. Top app bar with a back arrow and the title only, spanning the full window width. NO bottom navigation bar, NO drawer, NO FAB in this state.

**Component 1 - Top App Bar** (64dp tall, background #FAFAFB): back arrow, title "Offline sync" semibold title-large #0F172A.

**Component 2 - Offline Banner** (12dp radius, tertiaryContainer #FEF3C7, onTertiaryContainer #78350F, 12dp by 16dp padding): cloud-off icon and "You're offline. Everything on this device still opens; syncing resumes when you're back online."

**Component 3 - Summary Card** (16dp radius, white, 1dp #CBD5E1 border, 16dp padding): chips "Offline" (#FEF3C7, wifi-off icon) and "3 to sync" (neutral #E2E8F0). Three level tiles: "2" Centres, "5" Groups, "43" Clients. Caption "Offline, last synced 2 h ago". Full-width 48dp pill button "Sync when online" disabled (#E2E8F0 fill, #94A3B8 label, sync-disabled icon).

**Component 4 - On this device Card** (list_screen archetype): heading, Chip Row "Centres 2", "Groups 5", "Clients 43" selected. A 44dp rounded search field on #FAFAFB "Search 43 clients on this device". Client rows with 40dp #D1FAE5 initials avatars and a trailing chevron:
- "Irving Zamora", "1 loan, 1 savings, chosen", status "Out of date, synced 2 days ago" #D97706 with a history icon
- "FOTest Asha", "2 loans, 1 savings, 3 docs, via MARIPOSAS MONARCAS", "Synced 2 h ago" #059669
- "José Luis Hernández", "2 loans, 1 closed, via Las Margaritas", "Synced 2 h ago" #059669
- "María Guadalupe Torres", "1 loan, 2 savings, via MARIPOSAS MONARCAS", "Synced 2 h ago" #059669

**Component 5 - Drafts Note Card** (same card style, one row, 12dp by 16dp padding): edit-note icon #4338CA, text "Work you do offline is saved as drafts." #475569, and a trailing text link "Sync & Drafts" semibold #4338CA.

DO NOT show an error, a timeout or a retry action; being offline is a normal field condition, not a failure. DO NOT show uploads, payloads or queues on this screen. DO NOT render a bottom navigation bar or a FAB. DO NOT use em-dash characters anywhere.

Steady and capable: a warm amber banner states the condition once, and the full client list stays bright and usable underneath, showing the officer the device is ready for the field.

↑↑↑ MOCKUP PROMPT
