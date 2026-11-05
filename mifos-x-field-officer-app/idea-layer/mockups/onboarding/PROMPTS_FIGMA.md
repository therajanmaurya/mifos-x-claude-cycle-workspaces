# Onboarding — Figma Design Prompt

> Generated from `screens/onboarding/ui.yaml` + `mockups/onboarding/MOCKUP.md` by `/idea-feature-export onboarding`
> Design System: Material Design 3 on the shipped KptTheme (light scheme, Outfit)
> Generated: 2026-11-04T18:10:00Z

---

## 1. Frame Setup

- **Frames**: compact (Android 412 × 892), medium (840 × 1180 tablet portrait), expanded (1280 × 1024) — the
  device sizes are proportion references; every frame uses Fill layouts, never a phone column inside a wider canvas
- **Grid**: compact 4-column, 16dp gutter, 24dp margin (`spacing/xl`); expanded 2 panes, content max 1040dp
- **Status bar / safe area**: system, respected top and bottom
- **Chrome**: none — no top app bar, no bottom nav, no FAB, no drawer

---

## 2. Design Token Variables

### Colors (Light Mode — the KptTheme default)

| Variable Name | Value | Usage |
|---|---|---|
| `color/primary` | #4338CA | Next, Get started, active dot, Skip, links, checked switch track |
| `color/onPrimary` | #FFFFFF | button labels |
| `color/primaryContainer` | #E0E7FF | clients + privacy illustration panels |
| `color/secondary` | #059669 | shield icon |
| `color/secondaryContainer` | #D1FAE5 | offline illustration panel, no-client-data callout |
| `color/onSecondaryContainer` | #064E3B | callout text (Stitch render) |
| `color/tertiaryContainer` | #FEF3C7 | collections illustration panel |
| `color/background` | #FAFAFB | page background |
| `color/onSurface` | #0F172A | titles, switch labels |
| `color/onSurfaceVariant` | #475569 | body, lead, supporting text, settings caption |
| `color/surfaceVariant` | #E2E8F0 | unchecked switch track |
| `color/outline` | #94A3B8 | inactive dots, unchecked track border + thumb |
| `color/outlineVariant` | #CBD5E1 | divider between switch rows |
| `color/inverseSurface` | #1E293B | save-error snackbar |
| `color/inverseOnSurface` | #F1F5F9 | snackbar text |

### Colors (Dark Mode)

`design-tokens.yaml` extracts the light scheme only (KptTheme resolves `lightScheme` by default); dark values
come from `KptTheme` at runtime and are not authored here.

### Typography (Outfit, stock M3 scale)

| Style | Size | Weight | Line Height | Used by |
|---|:-:|:-:|:-:|---|
| headlineMedium | 28sp | SemiBold (render) | 36sp | intro_title, privacy_title |
| bodyLarge | 16sp | Normal | 24sp | intro_body, privacy_lead |
| titleMedium | 16sp | Medium | 24sp | switch labels |
| bodyMedium | 14sp | Normal | 20sp | switch supporting text, no_client_data_note |
| bodySmall | 12sp | Normal | 16sp | settings_later_note |
| labelLarge | 14sp | Medium | 20sp | Skip, Next, Get started, links |

### Spacing (`LocalSpacing`)

| Token | Value |
|---|:-:|
| `spacing/xs` | 4dp |
| `spacing/sm` | 8dp |
| `spacing/md` | 12dp |
| `spacing/lg` | 16dp |
| `spacing/xl` | 24dp |
| `spacing/xxl` | 32dp |
| `spacing/touchTargetMin` | 48dp |

### Corner Radius (ui.yaml `cornerRadius` names)

| Name | Used by |
|---|---|
| full (pill) | Next, Get started, Skip, dots, switch track |
| xl (large panel) | illustration panels |
| sm (small) | brand mark, callout, snackbar |

---

## 3. Auto Layout Structure

### intro_clients / intro_collections / intro_offline

```
Frame: onboarding_intro_{page} (Fill, Auto Layout Vertical, padding spacing/xl, fill color/background)
  ├─ TopRow (Fill x Hug, Horizontal, space-between)
  │   ├─ BrandMark (32 x 32dp, radius sm) — onboarding_brand_mark
  │   └─ TextButton "Skip" (Hug x 48dp, labelLarge, color/primary) — onboarding_skip
  ├─ Art (Fill x ~40% height, radius xl, fill primaryContainer | tertiaryContainer | secondaryContainer)
  │   └─ Illustration (decorative) — onboarding_illustration_{clients|collections|offline}
  ├─ Copy (Fill x Hug, Vertical, gap spacing/md)
  │   ├─ Title (headlineMedium, color/onSurface) — onboarding_title
  │   │   "Your clients, groups and centres — in the field" | "Collect repayments and run collection sheets" | "No signal? Keep working"
  │   └─ Body (bodyLarge, color/onSurfaceVariant) — onboarding_body
  └─ Controls (Fill x Hug, Vertical, gap spacing/lg, pinned bottom)
      ├─ PageIndicator (Horizontal, gap spacing/sm) — onboarding_page_indicator, current dot primary pill
      └─ Button "Next" (Fill x 48dp, radius full, color/primary, label onPrimary) — onboarding_next
Expanded: Frame becomes Horizontal — Art (Fill, start half) | Copy + Controls (Fill, end half), max 1040dp
```

### privacy

```
Frame: onboarding_privacy (Fill, Auto Layout Vertical, padding spacing/xl, fill color/background)
  ├─ Art (expanded only, start pane, radius xl, primaryContainer) — onboarding_illustration_privacy
  ├─ Heading (Vertical, gap spacing/md)
  │   ├─ "Help improve the app" (headlineMedium) — onboarding_privacy_title
  │   └─ "Both are off unless you turn them on. You can say no and still use everything." — onboarding_privacy_lead
  ├─ Choices (Vertical, divider color/outlineVariant)
  │   ├─ SwitchRow (Fill x ≥72dp) "Share usage analytics" + supporting text — onboarding_analytics_switch [OFF]
  │   └─ SwitchRow (Fill x ≥72dp) "Send crash reports" + supporting text — onboarding_crash_reports_switch [OFF]
  ├─ Reassurance (Vertical, gap spacing/sm)
  │   ├─ Callout (padding md/lg, radius sm, secondaryContainer, shield icon secondary)
  │   │   "Nothing about your clients, loans or savings is ever sent." — onboarding_no_client_data
  │   ├─ Link "Privacy policy" (48dp, primary, underline) — onboarding_privacy_policy
  │   ├─ Caption "You can change this later in Settings." (bodySmall) — onboarding_settings_later
  │   └─ Link "Connect to your Mifos instance" (48dp, primary, underline) — onboarding_connect_instance
  ├─ Controls (pinned bottom): PageIndicator (dot 4 active) · Button "Get started" (Fill x 48dp) — onboarding_get_started
  └─ Overlay: Snackbar "Couldn't save your choices. Try again." (inverseSurface, radius sm) — onboarding_save_error [save_failed only]
```

No loading / empty / error frames: every page is a content state; the only failure is the in-place
`save_failed` overlay above (ui.yaml `state_compositions.privacy`).

---

## 4. Component Variants

### button: next / get_started

| State | Background | Label | Opacity |
|---|---|---|:-:|
| Default | color/primary | color/onPrimary | 100% |
| Pressed | color/primary + ripple | color/onPrimary | 100% |
| Focused | color/primary + 2dp focus outline | color/onPrimary | 100% |
| Disabled (get_started while saving) | color/primary | color/onPrimary | 38% |

### switch: analytics_switch / crash_reports_switch

| State | Track | Thumb | Notes |
|---|---|---|---|
| Off (default) | color/surfaceVariant, 2dp color/outline border | color/outline, start | never pre-ticked |
| On | color/primary | color/onPrimary, end | after the officer's tap |
| Focused | + 2dp focus outline | — | whole row is one toggleable node |
| Disabled (saving) | 38% | 38% | cannot change what is being written |

### text_button / link: skip, privacy_policy_link, connect_instance_link

Default color/primary (underlined for links) · Pressed ripple · Focused outline · Disabled 38%
(`connect_instance_link` while saving). Minimum 48dp touch target.

### page_indicator

Current: 24 × 8dp pill color/primary · Other: 8dp outlined dot color/outline. Not interactive, not focusable.

### snackbar_host: save_error_snackbar

Hidden by default; visible only when `saveFailed`; polite live region.

---

## 5. Assets Required

### Icons

| Icon | Size | Usage | Style |
|---|:-:|---|:-:|
| shield_check | 20dp | no_client_data_note leading icon (color/secondary) | outlined |

### Images (ui.yaml `visual_assets[]`)

| Asset | Usage | Produced by |
|---|---|---|
| onboarding_brand_mark | intro pages, 32dp | `/idea-branding` from `design-system/branding/mifos-x-mark.svg` |
| onboarding_clients_illustration | intro_clients panel | `/idea-feature-stitch-art` |
| onboarding_collections_illustration | intro_collections panel | `/idea-feature-stitch-art` |
| onboarding_offline_illustration | intro_offline panel | `/idea-feature-stitch-art` |
| onboarding_privacy_illustration | privacy start pane (expanded) | `/idea-feature-stitch-art` |

---

## 6. Responsive Variants

| Breakpoint | Layout Changes |
|:-:|---|
| Compact (< 600dp) | single column, illustration ~40% height above the text, full-width primary button |
| Medium (600–839dp) | content centred at 560dp max width, stacked, larger illustration |
| Expanded (≥ 840dp) | two panes: illustration start half, copy / switches + controls end half, max 1040dp |

---

## Mood Palette Usage

`design-tokens.yaml` declares no `mood*` tokens — nothing to map (RULE-MOODPALETTE-USAGE-001 not applicable).
The `finance.*` tokens are unused here: onboarding shows no money.

## WCAG Contrast Audit

| Text / element | Background | Ratio | Required | Pass? |
|---|---|:-:|:-:|:-:|
| onSurface #0F172A (titles, labels) | background #FAFAFB | 17.11 | 4.5 | ✅ |
| onSurfaceVariant #475569 (body, supporting) | background #FAFAFB | 7.26 | 4.5 | ✅ |
| onPrimary #FFFFFF (button labels) | primary #4338CA | 7.90 | 4.5 | ✅ |
| primary #4338CA (Skip, links) | background #FAFAFB | 7.58 | 4.5 | ✅ |
| onSurface #0F172A (callout, ui.yaml) | secondaryContainer #D1FAE5 | 15.74 | 4.5 | ✅ |
| onSecondaryContainer #064E3B (callout, Stitch) | secondaryContainer #D1FAE5 | 8.57 | 4.5 | ✅ |
| inverseOnSurface #F1F5F9 (snackbar) | inverseSurface #1E293B | 13.35 | 4.5 | ✅ |
| outline #94A3B8 (inactive dot, OFF thumb/border — non-text) | background #FAFAFB | 2.46 | 3.0 | ❌ advisory |

The one failing pair is a non-text UI component (WCAG 1.4.11). The dots are non-interactive and the page is
also announced as "Page n of 4"; the OFF switch is identified by its label + On/Off state in one node. Flagged
for the implement-time design pass — not hidden.

## Motion

Pager page change: Android `FastOutSlowInInterpolator` (M3 standard) / iOS `CAMediaTimingFunction(name: .easeInEaseOut)`,
~300ms. No auto-advance.
