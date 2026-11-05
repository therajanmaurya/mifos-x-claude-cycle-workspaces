# Onboarding — Visual Mockup

> Auto-generated from `screens/onboarding/{ui,docs,demo-data}.yaml` by `/idea-feature-export onboarding`
> Design tokens: `design-system/design-tokens.yaml` · brand spec `design-system/DESIGN.md`
> Design tier consumed: **stitch** (RULE-UI-SOURCE-001 US9) — `mockups/onboarding/stitch/0{1..4}-onboarding-*`
> Variants = the per-state prompt set `screens/onboarding/prompts/*.md`: intro_clients · intro_collections · intro_offline · privacy
> Generated: 2026-11-04T18:08:00Z

---

## Shell (all variants)

Resolved from `app-shell.yaml` + `ui.yaml#shell`: **no top app bar · no bottom navigation · no FAB · no
drawer**. Full-bleed `background` surface, safe area respected top and bottom. Pre-auth first run, so there
is nothing to go back to and no tab to switch.

## Screen: OnboardingScreen (`pager`, `onboarding_step` archetype)

One screen, one `OnboardingViewModel`, four pages. Swipe = Next / back and never saves.

### State: intro_clients (page 1 of 4)

```
┌─────────────────────────────────────────┐
│ [X]                               Skip  │  brand_mark (32dp) · skip (primary text button)
│                                          │
│  ┌────────────────────────────────────┐  │
│  │  illustration — officer + clients   │  │  intro_illustration_clients
│  │  under a meeting tree, centre house │  │  primaryContainer panel, large radius
│  └────────────────────────────────────┘  │
│                                          │
│  Your clients, groups and centres —      │  intro_title (headlineMedium, onSurface)
│  in the field                            │
│  Look up a client, open a group or a     │  intro_body (bodyLarge, onSurfaceVariant)
│  centre and see their loans and savings, │
│  wherever your visits take you.          │
│                                          │
│  ▬ ○ ○ ○                                 │  page_indicator (current = primary pill)
│  [            Next            ]          │  next (primary pill, onPrimary label)
└─────────────────────────────────────────┘
```

### State: intro_collections (page 2 of 4)

```
┌─────────────────────────────────────────┐
│ [X]                               Skip  │
│  ┌────────────────────────────────────┐  │
│  │  illustration — centre meeting,     │  │  intro_illustration_collections
│  │  repayment on a phone, name list    │  │  tertiaryContainer panel
│  └────────────────────────────────────┘  │
│  Collect repayments and run collection   │  intro_title
│  sheets                                  │
│  Record repayments at the meeting and    │  intro_body
│  work through a centre's collection      │
│  sheet client by client.                 │
│  ○ ▬ ○ ○                                 │
│  [            Next            ]          │
└─────────────────────────────────────────┘
```

### State: intro_offline (page 3 of 4)

```
┌─────────────────────────────────────────┐
│ [X]                               Skip  │
│  ┌────────────────────────────────────┐  │
│  │  illustration — rural road, no      │  │  intro_illustration_offline
│  │  signal, cloud with sync arrow      │  │  secondaryContainer panel
│  └────────────────────────────────────┘  │
│  No signal? Keep working                 │  intro_title
│  Records you keep on the device open     │  intro_body
│  offline. What you capture is saved and  │
│  syncs when you're back online.          │
│  ○ ○ ▬ ○                                 │
│  [            Next            ]          │
└─────────────────────────────────────────┘
```

### State: privacy (page 4 of 4)

```
┌─────────────────────────────────────────┐
│  Help improve the app                    │  privacy_title (headlineMedium)
│  Both are off unless you turn them on.   │  privacy_lead (bodyLarge, onSurfaceVariant)
│  You can say no and still use everything.│
│                                          │
│  Share usage analytics            ( ○  ) │  analytics_switch — OFF (surfaceVariant track)
│  Which screens and features are used...  │    supporting text
│  ───────────────────────────────────────  │  outlineVariant hairline
│  Send crash reports               ( ○  ) │  crash_reports_switch — OFF
│  When the app crashes: the error, the... │
│                                          │
│  ┌────────────────────────────────────┐  │
│  │ ⛨ Nothing about your clients, loans │  │  no_client_data_note
│  │   or savings is ever sent.          │  │  secondaryContainer, shield in secondary
│  └────────────────────────────────────┘  │
│  Privacy policy                          │  privacy_policy_link (primary, underlined)
│  You can change this later in Settings.  │  settings_later_note (bodySmall)
│  Connect to your Mifos instance          │  connect_instance_link (primary, underlined)
│                                          │
│  ○ ○ ○ ▬                                 │
│  [         Get started         ]         │  get_started (primary pill)
└─────────────────────────────────────────┘
  overlay (save_failed only): [ Couldn't save your choices. Try again. ]   save_error_snackbar (inverseSurface)
```

In-place conditions (not extra states): **saving** disables Get started, both switches and the instance link;
**save_failed** shows `save_error_snackbar` and re-enables Get started.

### Component Hierarchy

```
OnboardingScreen/
├── Pager (onboarding_pager, background, padding xl)
│   ├── IntroPage × 3 (intro_clients · intro_collections · intro_offline)
│   │   ├── TopRow (space_between): brand_mark: image · skip: text_button
│   │   ├── Art: intro_illustration_{clients|collections|offline}: image (decorative)
│   │   ├── Copy: intro_title: text (heading) · intro_body: text
│   │   └── Controls (pinned bottom): page_indicator · next: button
│   └── PrivacyPage
│       ├── Art (expanded only): privacy_illustration: image (decorative)
│       ├── Heading: privacy_title · privacy_lead
│       ├── Choices (divider): analytics_switch: switch · crash_reports_switch: switch
│       ├── Reassurance: no_client_data_note · privacy_policy_link: link · settings_later_note · connect_instance_link: link
│       ├── Controls (pinned bottom): page_indicator · get_started: button
│       └── Overlay: save_error_snackbar: snackbar_host
```

### Dimensions

| Element | Size / spacing |
|---|---|
| page padding | spacing `xl` (24dp) horizontally; `xxl` (32dp) top/bottom in the Stitch render |
| brand_mark | 32dp square |
| tap targets (skip, next, switch rows, links, get_started) | ≥ `touchTargetMin` (48dp) |
| page_indicator | 4 dots, 8dp, gap `sm` (8dp); current dot a 24×8dp `primary` pill |
| intro illustration | ~40% of height on compact |
| primary button | full width on compact; capped and centred on medium; in the end pane on expanded |

### Responsive (RULE-MOCKUP-RESPONSIVE-001)

| Width | Layout |
|---|---|
| compact < 600dp | single column, illustration above the text, full-width primary button |
| medium 600–839dp | content centred at 560dp max width, illustration and text stacked, larger illustration |
| expanded ≥ 840dp | two panes — illustration on the start half, title/body (or the privacy switches) + controls on the end half; max content width 1040dp; `privacy_illustration` appears only here |

The delivered Stitch renders follow this: `01-onboarding-intro_clients/screen.png` is captured at the expanded
width and shows the two-pane layout (illustration start, copy + indicator + Next end).

### Interaction summary

| Control | Action | Result |
|---|---|---|
| skip | skip_to_privacy | privacy page; nothing saved |
| next / swipe left | next_page | next page |
| system back / swipe right | previous_page | previous page; on page 1 the app exits, nothing saved |
| analytics_switch / crash_reports_switch | toggle_analytics / toggle_crash_reports | in-memory only |
| privacy_policy_link | open_url | `https://mifos-products.pages.dev/mobile/field-officer/privacy/` in the browser |
| connect_instance_link | open_server_config | `serverConfig` (push; back returns here) |
| get_started | finish_onboarding | saves both choices, then `setFirstTimeState(false)` → `signin` |

### Demo content (demo-data.yaml)

Default privacy variant `onboarding_demo_privacy_default`: analytics OFF, crash reports OFF. Variant
`onboarding_demo_privacy_one_on` (crash_reports_only): analytics OFF, crash reports ON — what Get started stores
exactly.

### Notes on the delivered tier

- `04-onboarding-privacy/screen.png` is a 200×200 image, not a page capture; the full page is in
  `04-onboarding-privacy/code.html` (title, both switch rows, links, Get started and `lg:` two-pane rules present).
- The privacy Stitch prompt places the brand mark on page 4; `ui.yaml` scopes `brand_mark` to the intro pages —
  `ui.yaml` structure wins for implementation.
