---
ui_yaml_sha: 8fe572b87eadcf3bcde31eeef3ff1972bbe4eb1ac391c4523af799fec5e96d1c
design_md_hash: c1e7dbe50f7725a08e0369f4cb0659b8c1e56ac645d128a4c90c66b8618666ef
app_shell_hash: 89077f8f960080911cf9c2b934ba619c11591fcb24da55987a5a1bb79f349739
design_read_hash: b8351b69fe65d3e807e7686d56aa6c004cbea4c5b2bf145c0c7ae38c6ea0aa95
content_hash: f80aeeb3705dadbf6d5ef8b1d8606e28324d9a8aa0c6df1ab2bfc7e8edb30013

design_read_aesthetic: minimalist-ui
design_read_dials: {variance: 3, motion: 2, density: 6}
aesthetic_variant_override: null
archetype: onboarding_step

feature: onboarding
state: privacy
state_visibility: privacy

project_id: '10780096558615730514'
design_system_id: '9551377288795375599'

generated_by: stitch-prompt-build.ts v2.1.0
prompt_template_version: stitch-per-state-v3.1.0
craft_rules_version: v1.5.0
---

# onboarding — privacy state

> Auto-generated from screens/onboarding/ui.yaml @ SHA 6358a173f6592a0f
> Stitch DesignSystem: 9551377288795375599
> DO NOT redeclare colors / fonts / spacing — they live in DESIGN.md.

↓↓↓ MOCKUP PROMPT

Design the privacy state of the onboarding screen for **Mifos X Field Officer**, a field app for microfinance loan officers.

Palette: background #FAFAFB, onSurface #0F172A, primary #4338CA, onPrimary #FFFFFF, primaryContainer #E0E7FF, onPrimaryContainer #1F1D75, secondary #059669, secondaryContainer #D1FAE5, onSecondaryContainer #064E3B, tertiary #D97706, onSurfaceVariant #475569, outline #94A3B8, outlineVariant #CBD5E1, inverseSurface #1E293B.

Shell: no top bar, no bottom nav, no tabs, no drawer, no FAB. The onboarding pager is a full-bleed pre-authentication surface; all chrome is suppressed on every onboarding page.

The page has THREE regions stacked in a full-height column: a fixed top row, a scrolling content area that takes all remaining height, and a FIXED bottom action bar pinned to the bottom edge of the viewport (sticky footer, never scrolls, always fully visible). Both finishing buttons live in that fixed bar and must be visible without any scrolling.

**Component 1 - Row** (top region, full width inside 24dp side insets, min-height 48dp, top safe-area respected, fixed, does not scroll): Left side only: the Mifos X brand mark, exactly 32dp square, drawn straight on the page background with NO tile or dark container behind it: a square split by two white diagonal strokes into four triangles, top triangle lime green, bottom triangle green, left triangle blue, right triangle sky blue; never any other glyph. No Skip on this page; the row keeps its 48dp height so the mark sits exactly where it sits on the intro pages. onboarding_step archetype: final page of the four-page pager.

**Component 2 - Hero** (hidden at compact and md, display none; at lg: start half of the two-column scrolling row, flex-1, 24dp corner radius, background #E0E7FF, 4:3 aspect ratio): Decorative flat illustration: an officer's Android phone showing a two-row toggle list with BOTH switches OFF, a closed padlock in #4338CA at its lower left and a small shield in #059669 at its lower right. No client names, account numbers or amounts anywhere.

**Component 3 - Text** (scrolling content, full width inside 24dp insets, top margin 16dp): Headline "Help improve the app" Outfit SemiBold 28sp line-height 36dp #0F172A, left-aligned, max 3 lines. At lg: font-size 32sp line-height 40dp.

**Component 4 - Text** (scrolling content, top margin 16dp): Body "Both are off unless you turn them on. Allow both in one tap, or choose below, you can still use everything." Outfit Regular 16sp line-height 24dp #475569, left-aligned.

**Component 5 - Switch** (scrolling content, full width, top margin 16dp, min touch-target height 48dp, 12dp vertical padding): Switch row rendered OFF, unchecked, aria-checked false: thumb at the leading edge, track #CBD5E1, thumb #FFFFFF. Leading column: label "Share usage analytics" Outfit Medium 16sp #0F172A; supporting text "Which screens and features are used, and how often. No client names, account numbers or amounts." Outfit Regular 13sp line-height 20dp #475569. Trailing: switch 52dp wide 32dp tall, pill track.

**Component 6 - Divider** (scrolling content, full width): 1dp horizontal rule #CBD5E1.

**Component 7 - Switch** (scrolling content, full width, min touch-target height 48dp, 12dp vertical padding): Switch row rendered OFF, unchecked, aria-checked false, same spec as Component 5. Label "Send crash reports"; supporting text "When the app crashes: the error, the app version and the device model, so we can fix it. No client data."

**Component 8 - Card** (scrolling content, full width, top margin 16dp, 12dp corner radius, background #D1FAE5, 16dp internal padding): Row: leading shield icon 24dp #064E3B, 12dp gap, text "Nothing about your clients, loans or savings is ever sent." Outfit Regular 14sp line-height 20dp #064E3B.

**Component 9 - Text** (scrolling content, full width, top margin 16dp, left-aligned): Agreement line Outfit Regular 14sp line-height 20dp: "By using our service you accept our Terms & Conditions and Privacy Policy." as ONE continuous text run where "Terms & Conditions" is an inline link span (#4338CA, underlined) and "Privacy Policy" is a second inline link span (#4338CA, underlined); all other words #475569. Do not split it, reword it or reorder it, and do not move it into the bottom bar.

**Component 10 - Text** (scrolling content, top margin 16dp): Caption "You can change this later in Settings." Outfit Regular 13sp line-height 20dp #475569, left-aligned.

**Component 11 - Text Link** (scrolling content, the LAST scrolling item, top margin 8dp, min touch-target height 48dp): Text Button "Connect to your Mifos instance" Outfit Medium 14sp #4338CA, left-aligned. It may sit below the fold on a phone, reached by scrolling. on_click action open_server_config.

**Component 12 - Page Indicator** (bottom action bar, first row, CENTRED horizontally, padding-top 16dp): Four dots, 8dp gap. Dots 1, 2, 3: 8dp circles, fill #CBD5E1. Dot 4 (active, this page): pill 24dp wide 8dp tall, background #4338CA.

**Component 13 - Button** (bottom action bar, FULL WIDTH of the bar inside 24dp insets at every width, top margin 16dp, 48dp tall, 999dp corner radius pill): Filled primary button "Allow and get started" Outfit SemiBold 16sp #FFFFFF, background #4338CA, label centred. on_click action allow_all_and_finish.

**Component 14 - Outlined Button** (bottom action bar, directly below Component 13, top margin 12dp, bottom 16dp plus safe-area inset, 48dp tall, 999dp corner radius pill, identical width to Component 13): Outlined button "Continue without sharing" Outfit SemiBold 16sp #4338CA, transparent fill, border 1dp #94A3B8, label centred. As prominent in height and width as Component 13, never a text link, never greyed. on_click action continue_with_choices.

Responsive layout: phone-first single column at compact width; the Hero is hidden at compact and md; the scrolling area holds Components 3 to 11 and the fixed bottom bar holds Components 12 to 14 at full content width. At md: (medium) the column is centred with a comfortable max content width. At lg: (expanded) the content width is capped wider, the scrolling area becomes a two-column row with the Hero on the start half and Components 3 to 11 on the end half, and the fixed bottom bar sits ONLY under the end (text) column, the space under the Hero stays empty. No fixed-width root element, no max-width cap at phone width.

DO NOT use em-dash anywhere in text. DO NOT make any headline >3 lines or any subtitle >25 words. DO NOT break the page theme between sections. DO NOT place light text on light buttons or dark text on dark buttons.

The indigo #4338CA on the active dot, the pinned primary button and the inline agreement links anchors the privacy moment in a calm, trustworthy register, while the emerald #D1FAE5 card reassures the officer that client data never travels and both choices stay equally easy.

↑↑↑ MOCKUP PROMPT
