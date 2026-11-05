---
ui_yaml_sha: 8fe572b87eadcf3bcde31eeef3ff1972bbe4eb1ac391c4523af799fec5e96d1c
design_md_hash: c1e7dbe50f7725a08e0369f4cb0659b8c1e56ac645d128a4c90c66b8618666ef
app_shell_hash: 89077f8f960080911cf9c2b934ba619c11591fcb24da55987a5a1bb79f349739
design_read_hash: b8351b69fe65d3e807e7686d56aa6c004cbea4c5b2bf145c0c7ae38c6ea0aa95
content_hash: 078847049b2f13920e5f17c3a5e13be23c98672448a5fdf2f306bd38af097e67

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 6}
aesthetic_variant_override: null
archetype: onboarding_step

feature: onboarding
state: intro_collections
state_visibility: intro_collections

project_id: '10780096558615730514'
design_system_id: '9551377288795375599'

generated_by: stitch-prompt-build.ts v2.1.0
prompt_template_version: stitch-per-state-v3.1.0
craft_rules_version: v1.5.0
---

# onboarding — intro_collections state

> Auto-generated from screens/onboarding/ui.yaml @ SHA e568cbd8d4432f0d
> Stitch DesignSystem: 9551377288795375599
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the intro_collections state of the onboarding screen for **Mifos X Field Officer**, a field app for microfinance loan officers.

Palette: background #FAFAFB, onSurface #0F172A, primary #4338CA, onPrimary #FFFFFF, primaryContainer #E0E7FF, onPrimaryContainer #1F1D75, secondary #059669, secondaryContainer #D1FAE5, tertiary #D97706, tertiaryContainer #FEF3C7, onSurfaceVariant #475569, outline #94A3B8, outlineVariant #CBD5E1, inverseSurface #1E293B.

Shell: no top bar, no bottom nav, no tabs, no drawer, no FAB. The onboarding pager is a full-bleed pre-authentication surface; all chrome is suppressed on every onboarding page.

The page has THREE regions stacked in a full-height column: a fixed top row, a scrolling content area that takes all remaining height, and a FIXED bottom action bar pinned to the bottom edge of the viewport (sticky footer, never scrolls, always fully visible). The bottom action bar is NOT part of the copy: it sits at the very bottom of the screen (sticky bottom-0, margin-top auto), all free whitespace goes ABOVE it, and Next is never placed directly under the body text. The page dots are CENTRED in the bar, not left-aligned.

**Component 1 - Row** (top region, full width inside 24dp side insets, min-height 48dp, top safe-area respected, fixed, does not scroll): Left side: the Mifos X brand mark, exactly 32dp square, drawn straight on the page background with NO tile or rounded container behind it: a square split by two white diagonal strokes into four triangles, top triangle lime green, bottom triangle green, left triangle blue, right triangle sky blue. It is the only logo on the page; never a letter, diamond, plus sign, shield or other glyph, never larger than 32dp. Right side: Text Button "Skip" Outfit Medium 15sp #4338CA, transparent background, pill touch target 48dp tall minimum 48dp wide, on_click action skip_to_privacy. onboarding_step archetype: this top row sits in the same place on every onboarding page.

**Component 2 - Hero** (scrolling content, full width inside 24dp insets, top margin 16dp, 24dp corner radius, background #FEF3C7, 4:3 aspect ratio): Flat illustration: a centre meeting outdoors where a loan officer records a repayment on a phone while a client hands over cash; beside them a short checklist of names with tick marks suggests the collection sheet. Amber #D97706 and indigo #4338CA accents, emerald #059669 ticks. No readable names or amounts, no text overlaid.

**Component 3 - Text** (scrolling content, full width inside 24dp insets, top margin 24dp): Headline "Collect repayments and run collection sheets" Outfit SemiBold 28sp line-height 36dp #0F172A, left-aligned, max 3 lines. At lg: font-size 32sp line-height 40dp.

**Component 4 - Text** (scrolling content, full width inside 24dp insets, top margin 12dp): Body "Record repayments at the meeting and work through a centre's collection sheet client by client." Outfit Regular 16sp line-height 24dp #475569, left-aligned. At lg: font-size 18sp line-height 28dp.

**Component 5 - Page Indicator** (bottom action bar, first row, CENTRED horizontally, padding-top 16dp): Four dots in a horizontal row, 8dp gap. Dot 2 (active, this page): pill shape 24dp wide 8dp tall, background #4338CA. Dots 1, 3, 4: each 8dp wide 8dp tall circular, fill #CBD5E1. The row is centred in the bar at every width.

**Component 6 - Button** (bottom action bar, second row, FULL WIDTH of the bar inside 24dp insets at every width, top margin 16dp, bottom 16dp plus safe-area inset, 48dp tall, 999dp corner radius pill): Filled button "Next" Outfit SemiBold 16sp #FFFFFF, background #4338CA, label centred. Pinned to the bottom of the screen together with Component 5; it never moves when the content above scrolls. on_click action next_page.

Responsive layout: phone-first single column at compact width, Hero above the headline and body in the scrolling area, the bottom action bar full content width. At md: (medium) the whole column is centred with a comfortable max content width, the Hero grows, the bottom bar stays full width of that column. At lg: (expanded) the content width is capped wider and the scrolling area becomes a two-column row: Hero on the start half, headline and body on the end half, vertically centred; the bottom action bar (centred dots + full-width Next) sits ONLY under the end (text) column, the space under the Hero stays empty. No fixed-width root element, no max-width cap at phone width.

DO NOT use em-dash anywhere in text. DO NOT make any headline >3 lines or any subtitle >25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

The indigo #4338CA on the active page dot and the pinned Next button keeps the screen calm and trustworthy, while the warm amber #FEF3C7 illustration panel gives the collections page a grounded, practical feel for the work done at each meeting.

↑↑↑ MOCKUP PROMPT
