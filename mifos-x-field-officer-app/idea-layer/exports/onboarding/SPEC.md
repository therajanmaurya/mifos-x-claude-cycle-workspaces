<!--
generated_by: /idea-feature-export
generated_at: 2026-11-05T06:40:00Z
feature_id: onboarding
generated_from_feature_version: "1.0"
generated_from_contract_version: "—"
prior_version: "2026-11-05T00:50:00Z"
sources:
  - screens/onboarding/docs.yaml
  - screens/onboarding/ui.yaml
  - screens/onboarding/api.yaml
  - screens/onboarding/flow.yaml
  - screens/onboarding/data-flow.yaml
  - screens/onboarding/demo-data.yaml
  - screens/onboarding/tests.yaml
  - _strings/strings.yaml (screens.onboarding.*)
  - design-system/design-tokens.yaml
  - design-system/app-shell.yaml
  - REQUIREMENTS.md (FR-ONB-01..08, NFR-ONB-01, FR-SET-PRIV-01)
design_tier_consumed: stitch          # RULE-UI-SOURCE-001 US9: all 4 states — mockups/onboarding/stitch/0{1..4}-onboarding-*
regen_reason: "2026-11-05 operator design feedback (FR-ONB-08): fixed bottom action bar on every page; shared-axis-X page transition (motion block); 32dp brand mark on every page incl. privacy; agreement_text moved into the scrolling content; save_error_snackbar → save_failed_text (onboarding_save_failed) in the bar; 24 test scenarios"
-->

# SPEC — Onboarding

First-run onboarding, shown ONCE on a fresh install before sign-in. Three intro pages say what the app is
for (clients, groups and centres in the field · repayments and collection sheets · offline, sync later), then
a privacy page asks — with both switches OFF — whether to share usage analytics and send crash reports.
Two equally visible buttons finish the privacy page: **Allow and get started** (filled primary) turns both
consents ON and saves them; **Continue without sharing / Continue with my choices** (outlined, same size)
saves the switches exactly as shown. Either button marks onboarding done and opens sign-in. An agreement
line in the privacy content — "By using our service you accept our Terms & Conditions and Privacy Policy." —
links both documents in-app. Skip on an intro page jumps to the privacy page so consent is never skipped
silently. Every page has a fixed top row (32dp Mifos X mark), a scrolling content area, and a FIXED bottom
action bar; page content moves with the shared-axis-X transition.

| | |
|---|---|
| Feature id | `onboarding` |
| Module | `feature/onboarding` (fork module) |
| Route | `OnboardingRoute` (no params) — the `RootNavState.ShowOnboarding` destination |
| Bottom nav | **no** — full screen, no top bar, no drawer, no FAB (`ui.yaml#shell`) |
| Business logic | `composite` — `local_only_prefs`, `OFFLINE_LOCAL_ONLY`; no network |
| Version | 1.0 |

## Decisions (docs.yaml)

| id | decision |
|---|---|
| shown-once-before-signin | RootNav `ShowOnboarding` destination; either privacy button → `setFirstTimeState(false)` → RootNav resolves to Auth; sign-out never resets it |
| consent-off-until-chosen | both switches start OFF, held in memory; Allow and get started saves both ON; Continue saves as shown; leaving without either saves nothing and onboarding shows again |
| consent-allow-or-continue-without | two EQUALLY VISIBLE buttons: `allow_get_started` (filled, saves both true); `continue_choices` (outlined, saves as shown — label "Continue without sharing" when both off, "Continue with my choices" when either on); the decline path is a full button, never a buried link |
| agreement-line-terms-and-privacy | `agreement_text` in the scrolling content (below the no-client-data note, above "You can change this later in Settings."): Terms & Conditions → `AppOrgLinks["terms"]`, Privacy Policy → `AppPrivacyConfig.PRIVACY_POLICY_URL`, both in-app; ONE `Text` with inline `LinkAnnotation` spans, tagged `onboarding_agreement`; spans tapped by text |
| fixed-bottom-action-bar | three regions on every page: fixed top row (48dp min) · scrolling content · FIXED bottom bar. Intro bar: centred dots, full-width Next. Privacy bar: centred dots, save-failed text when shown, full-width filled Allow and get started, full-width outlined Continue. Expanded: the bar sits under the end (text) pane |
| shared-axis-page-transition | content changes with `KptSharedAxis` (forward when advancing, back when going back; `MaterialTheme.motion.durationLong1`, 450ms); top row + bottom bar never slide; the bar's buttons crossfade (`durationMedium1`, 250ms) when privacy swaps Next for the two finishing buttons |
| brand-mark-32dp | the Mifos X mark is 32dp (`spacing.xxl`) on every page incl. privacy; the top row keeps a 48dp minimum height so the mark does not jump where Skip is hidden |
| skip-lands-on-privacy | Skip on any intro page jumps to the privacy page, never past it |
| consent-applies-through-existing-applier | onboarding only writes the two stored choices; `PrivacyConsentApplier` switches collection on/off — no Firebase dependency here |
| instance-link-optional | "Connect to your Mifos instance" → `serverConfig`; back returns to the privacy page |
| full-screen-shell | no top app bar, no bottom navigation, no drawer |
| first-run-via-template-seam | fresh install reaches `ShowOnboarding` via `app-profile/app.yaml#security.first_run_onboarding` → `AppSecurityConfig.FIRST_RUN_ONBOARDING` → `UserData.DEFAULT.firstTimeUser` (template PR #316, 3dd68cd9) |
| settings-privacy-in-same-pass | FR-SET-PRIV-01 (Settings → Privacy sheet) ported from the template `PrivacySheet` into the fork-owned `feature/settings` in the same pass |

## App-Shell

Resolved against `design-system/app-shell.yaml` (defaults: bottom nav visible, top bar visible) with the
`ui.yaml#shell` override: **bottom navigation hidden · top app bar hidden · FAB hidden · drawer not
accessible**. Safe drawing padding on all edges. The app-level snackbar host is not used; the privacy page
shows its save error inline in the bottom bar (`save_failed_text`).

## Layout + Motion (ui.yaml#layout.regions, #motion)

| Region | Contents | Behaviour |
|---|---|---|
| top_row | brand_mark (32dp, top start) · skip (top end, intro only) | fixed, `heightIn(min = 48dp)` on every page |
| content | intro: illustration + title + body · privacy: title, lead, 2 switch rows, no-client-data note, agreement line, settings note, connect link | the ONLY region that scrolls and the ONLY region that slides (shared-axis X) |
| bottom_bar | intro: centred dots + full-width Next · privacy: centred dots, save_failed_text, Allow and get started (filled), Continue (outlined) | fixed, never scrolls, never slides; buttons crossfade on the privacy swap; expanded → under the end pane |

Responsive: compact < 600dp full content width; medium 600–839dp content centred at 560dp; expanded ≥ 840dp two
panes capped at 1040dp (illustration start, text end; privacy illustration expanded-only).

## Screens

| Screen | ViewModel | States (ui.yaml) | Description |
|---|---|---|---|
| `OnboardingScreen` | `OnboardingViewModel` | intro_clients, intro_collections, intro_offline, privacy | One screen, one ViewModel: a four-page pager (three intro pages + privacy) — a wizard in pages, not four routes |

All four states are `content` — nothing loads and nothing fails except the one local write on the privacy
buttons, handled in place (`state_compositions.privacy`: `saving` disables both buttons, both switches and
the instance link; `save_failed` shows `save_failed_text` and re-enables both buttons).

## Components (ui.yaml → testTag)

| Component | testTag | States | Contents |
|---|---|---|---|
| pager | `onboarding_pager` | all | 4 pages; swipe = Next / back, never saves; back on page 1 → system, nothing stored |
| skip | `onboarding_skip` | intro × 3 | "Skip" (a11y "Skip to the privacy choices") → privacy page |
| brand_mark | `onboarding_brand_mark` | all 4 | Mifos X mark, **32dp**, top start (`onboarding_brand_mark` asset, from `branding/mifos-x-mark.svg`) |
| intro_illustration_clients / _collections / _offline | `onboarding_illustration_clients` / `_collections` / `_offline` | one each | decorative; rounded `extraLarge` panel, 4:3 |
| intro_title | `onboarding_title` | intro × 3 | "Your clients, groups and centres — in the field" · "Collect repayments and run collection sheets" · "No signal? Keep working" (heading) |
| intro_body | `onboarding_body` | intro × 3 | the matching body line from `screens.onboarding.*_body` |
| page_indicator | `onboarding_page_indicator` | all | 4 dots in the bottom bar, centred; current = 24dp `primary` pill, others 8dp `outlineVariant`; announced "Page n of 4" |
| next | `onboarding_next` | intro × 3 | "Next" — full-width pill in the bottom bar |
| privacy_illustration | `onboarding_illustration_privacy` | privacy | decorative; **expanded only** (start pane) |
| privacy_title / privacy_lead | `onboarding_privacy_title` / `onboarding_privacy_lead` | privacy | "Help improve the app" · "Both are off unless you turn them on. Allow both in one tap, or choose below — you can still use everything." |
| analytics_switch | `onboarding_analytics_switch` | privacy | "Share usage analytics" + supporting text; default **OFF**; one toggleable node |
| crash_reports_switch | `onboarding_crash_reports_switch` | privacy | "Send crash reports" + supporting text; default **OFF** |
| no_client_data_note | `onboarding_no_client_data` | privacy | "Nothing about your clients, loans or savings is ever sent." — `secondaryContainer`, shield icon |
| agreement_text | `onboarding_agreement` | privacy | scrolling content; ONE `Text` with inline `LinkAnnotation` spans: "By using our service you accept our **Terms & Conditions** and **Privacy Policy**." — tapped by text |
| settings_later_note | `onboarding_settings_later` | privacy | "You can change this later in Settings." — backed by FR-SET-PRIV-01 |
| connect_instance_link | `onboarding_connect_instance` | privacy | "Connect to your Mifos instance" → `serverConfig`; last scrolling item |
| save_failed_text | `onboarding_save_failed` | privacy (save_failed) | "Couldn't save your choices. Try again." — `error` colour, in the bottom bar above the buttons, polite live region |
| allow_get_started | `onboarding_allow_get_started` | privacy | "Allow and get started" — filled primary, full-width, bottom bar; saves both consents ON, then `setFirstTimeState(false)` LAST |
| continue_choices | `onboarding_continue_choices` | privacy | outlined, full-width, same size, bottom bar; label "Continue without sharing" (both off) / "Continue with my choices" (either on); saves switches as shown |

## State Model

### OnboardingViewModel

- **State**: OnboardingState — page: OnboardingPage, analytics: Boolean, crashReports: Boolean, saving: Boolean, saveFailed: Boolean
- **Defaults**: page = `OnboardingPage.Clients` · analytics = false · crashReports = false · saving = false · saveFailed = false
- **Derived**: continueLabel = `if (analytics || crashReports) ContinueWithChoices else ContinueWithout`
- **ScreenState**: OnboardingPage — Clients, Collections, Offline, Privacy
- **Errors**: OnboardingError — LocalWriteFailed (retry=true, `screens.onboarding.save_failed`)
- **Events**: OnboardingEvent — OpenUrlInApp(url: String), OpenServerConfig, ExitApp
- **Actions**: Next (Tap Next / swipe left) · Back (System back / swipe right) · Skip (Tap Skip) · SetAnalytics(granted: Boolean) · SetCrashReports(granted: Boolean) · OpenTerms ("Terms & Conditions" span) · OpenPrivacyPolicy ("Privacy Policy" span) · OpenServerConfig (Connect link) · AllowAll (Allow and get started) · ContinueWithChoices (Continue)
- **DI**: UserDataRepository · UrlLauncher

| vm_action | signature | mutation / effect | error handling |
|---|---|---|---|
| NextPage | `fun next()` | page + 1 (max privacy) | AlreadyOnLastPage → no-op |
| PreviousPage | `fun back()` | page − 1; page 1 → `ExitApp`, nothing saved | FirstPage → system closes app, both consents stay off |
| Skip | `fun skip()` | page = privacy | AlreadyOnPrivacy → no-op |
| AnalyticsToggled | `fun setAnalytics(granted: Boolean)` | analytics = granted (memory); continueLabel derived | disabled while saving |
| CrashReportsToggled | `fun setCrashReports(granted: Boolean)` | crashReports = granted (memory); continueLabel derived | disabled while saving |
| OpenTerms | `fun openTerms()` | `OpenUrlInApp(AppOrgLinks["terms"])` → UrlLauncher.launchInApp | NoBrowserAvailable caught; page unchanged |
| OpenPrivacyPolicy | `fun openPrivacyPolicy()` | `OpenUrlInApp(AppPrivacyConfig.PRIVACY_POLICY_URL)` → UrlLauncher.launchInApp | NoBrowserAvailable caught; page unchanged |
| OpenServerConfig | `fun openServerConfig()` | `OpenServerConfig` → ServerConfigRoute | disabled while saving |
| AllowAll | `suspend fun allowAll(): Result<Unit>` | analytics = true; crashReports = true; saving = true → `setAnalyticsConsent(true)` → `setCrashReportingConsent(true)` → `setFirstTimeState(false)` LAST | LocalWriteFailed → saving=false, saveFailed=true, save_failed_text; `setFirstTimeState` not called |
| ContinueWithChoices | `suspend fun continueWithChoices(): Result<Unit>` | saving = true → `setAnalyticsConsent(analytics)` → `setCrashReportingConsent(crashReports)` → `setFirstTimeState(false)` LAST | LocalWriteFailed → saving=false, saveFailed=true, save_failed_text; `setFirstTimeState` not called |

## Capabilities

### key-value-preferences

`multiplatform-settings` 1.3.0 (android · ios · desktop · web) through `core/datastore` via
`UserDataRepository`: on **Allow and get started** — `setAnalyticsConsent(true)`, `setCrashReportingConsent(true)`, then
`setFirstTimeState(false)` LAST; on **Continue** — `setAnalyticsConsent(analytics)`, `setCrashReportingConsent(crashReports)`,
then `setFirstTimeState(false)` LAST. Permission: none. Error case: `LocalWriteFailed`.

### open-url

`cmp-open-url` 3.5.34 (kmptoolkit) via `UrlLauncher.launchInApp` (core-base/platform). Used by both agreement
links: `AppOrgLinks["terms"]` (Terms & Conditions) and `AppPrivacyConfig.PRIVACY_POLICY_URL` (Privacy Policy).
Both open in-app; closing returns to the privacy page with switches unchanged. Permission: none.
Error case: `NoBrowserAvailable` (caught inline; privacy page stays unchanged).

### motion

`core-base/ui` `KptSharedAxis` + `MaterialTheme.motion` (template motion system, `core-base/ui/MOTION.md`) —
no feature-local animation spec.

## API Endpoints (0)

| Function | Method | Params | Response | Errors | Table |
|---|---|---|---|---|---|
| (none) | — | — | — | — | — |

Pre-auth and local-only — no Fineract call. Local reads and writes are in `API.md`.

## Dependencies (Tier 2)

| Feature | Type | Required | Check |
|---|---|---|---|
| signin | navigation | true | feature/signin exists — Allow and get started / Continue land there via RootNav Auth |
| serverConfig | navigation | false | feature/settings ServerConfigRoute exists (the optional Connect to your Mifos instance link) |
| settings | data | false | feature/settings PrivacySheet — FR-SET-PRIV-01, backs settings_later_note (in progress) |

Services: `UserDataRepository` · `UrlLauncher` · shared entity `UserData`.

## Navigation (flow.yaml)

- **Route**: OnboardingRoute()
- **From**: rootNav — `RootNavState.ShowOnboarding` (`userData.firstTimeUser == true`, RootNavViewModel.kt:56)
- **To**: signin, serverConfig

| Trigger | Target | Type |
|---|---|---|
| Allow and get started saved | signin | replace_root (RootNav resolves to Auth; never shown again; both consents ON) |
| Continue saved | signin | replace_root (RootNav resolves to Auth; never shown again; consents as shown) |
| Connect to your Mifos instance | serverConfig | push (back returns with switch values kept) |
| "Terms & Conditions" span in agreement_text | `AppOrgLinks["terms"]` | in-app (UrlLauncher.launchInApp) |
| "Privacy Policy" span in agreement_text | `AppPrivacyConfig.PRIVACY_POLICY_URL` | in-app (UrlLauncher.launchInApp) |
| System back on page 1 | — | exit_app (nothing saved) |

Transitions (each page change animates the content region with shared-axis X): next_1 / next_2 / next_3 (intro
→ … → privacy) · skip (any intro → privacy) · back_2 / back_3 / back_4 · toggle · allow_get_started ·
continue_choices · save_failed · open_server_config · open_terms · open_privacy_policy. Journey
`field-officer-first-run`.

## Flow Logic (4 decisions)

| Decision | Condition | True Path | False Path | Impl |
|---|---|---|---|---|
| allow_get_started saved | all three writes succeed | signin (replace_root); both consents ON | stay on privacy, save_failed_text | `OnboardingViewModel:allowAll()` → RootNavViewModel (firstTimeUser=false) |
| continue_choices saved | all three writes succeed | signin (replace_root); consents as shown | stay on privacy, save_failed_text | `OnboardingViewModel:continueWithChoices()` → RootNavViewModel (firstTimeUser=false) |
| connect_instance_link | tapped on privacy page | serverConfig (push) | — | `OnboardingViewModel:openServerConfig()` → `OnboardingEvent.OpenServerConfig` |
| system back on page 1 | page == Clients | exit app, nothing saved | previous page | `OnboardingViewModel:back()` |

## Design (Stitch, consumed per state)

Full-bleed `background` surface, no chrome. Every page: a small 32dp Mifos X mark top-start in a 48dp row
(Skip top-end on the intro pages). Intro pages: a large rounded illustration panel, headline-medium title and
body-large copy in the scrolling area; the centred 4-dot indicator and a full-width indigo `primary` pill
"Next" pinned in the fixed bottom bar. Privacy page: title + lead, two switch rows separated by an
`outlineVariant` hairline with both tracks OFF, the emerald `secondaryContainer` reassurance callout with a
shield icon, the agreement line ("By using our service you accept our Terms & Conditions and Privacy Policy."
with both spans underlined in `primary`), the settings caption and the Connect link — all scrolling — then
the fixed bar: centred dots, `allow_get_started` (filled `primary`) above `continue_choices` (outlined), both
full-width. Expanded (≥ 840dp): two panes, illustration on the start half, the bar under the end pane, content
capped at 1040dp. All four mockups render responsively (`mockups/onboarding/stitch/MANIFEST.yaml`, design
system 9551377288795375599).

## Testing

`tests.yaml` — 24 scenarios (8 high · 13 medium · 3 low). Implement as `OnboardingViewModelTest` (paging,
skip, in-memory toggles, AllowAll saves both true, ContinueWithChoices saves as shown, write order with
`setFirstTimeState` last, LocalWriteFailed), `OnboardingScreenUiTest` (testTags, both switches OFF, both
buttons present and equally sized in the bottom bar, agreement_text with link spans, brand mark on every page,
expanded layout), previews + Roborazzi goldens per state, Maestro `happy_path`.

| ID | Scenario | Priority |
|---|---|---|
| intro_clients_fresh_install_opens_onboarding | fresh install opens onboarding page 1 before sign-in | high |
| intro_clients_next_through_to_privacy | Next ×3 reaches privacy with both switches OFF; both buttons visible, same size; agreement line in the scrolling content | high |
| intro_clients_skip_lands_on_privacy | Skip opens privacy directly, nothing saved; sign-in not reached until a button is tapped | high |
| intro_collections_back_returns_to_clients | back on page 2 shows page 1, app stays open, nothing saved | medium |
| intro_offline_swipe_matches_next | swipe left on page 3 equals Next, nothing stored | medium |
| intro_clients_bottom_bar_fixed | dots (centred) + full-width Next stay pinned at the bottom while content scrolls; same position on pages 1–3 | medium |
| intro_clients_page_transition_shared_axis | Next slides content forward (KptSharedAxis, 450ms), back slides it back; top row + bottom bar do not move | medium |
| privacy_allow_get_started_saves_both_on | Allow and get started with both switches off: both consents stored true; `setFirstTimeState` last; sign-in opens | high |
| privacy_finishing_buttons_visible_without_scroll | on a 360×640 phone both finishing buttons are fully visible with no scroll; buttons crossfade in (250ms); Connect link may need a scroll | high |
| privacy_continue_without_saves_both_off | Continue (both off): both consents false; `setFirstTimeState` last; sign-in opens; no Analytics/Crashlytics | high |
| privacy_continue_with_one_on_saves_crash_reports_only | crash reports ON, analytics OFF → Continue: Crashlytics on, Analytics off; relaunch opens sign-in; button reads "Continue with my choices" | high |
| privacy_continue_label_follows_switches | analytics ON → "Continue with my choices"; back to both OFF → "Continue without sharing"; allow_get_started label constant | medium |
| privacy_shown_once_after_finishing | relaunch after Allow/Continue opens sign-in, not onboarding | high |
| privacy_consent_survives_sign_out | sign-out shows sign-in, stored consent still true | medium |
| intro_clients_leave_without_choosing | back from page 1 saves nothing; onboarding shows again on relaunch | medium |
| privacy_back_keeps_switch_values_in_memory | back then Next: switch value kept in memory, not yet saved | medium |
| privacy_save_failed_keeps_page | write throws → `onboarding_save_failed` shows in the bottom bar; both buttons re-enabled; not marked done | medium |
| privacy_open_terms_in_app | tap "Terms & Conditions" inside `onboarding_agreement` → opens `AppOrgLinks["terms"]` in-app; closing returns to privacy page, switches unchanged | medium |
| privacy_open_privacy_policy_in_app | tap "Privacy Policy" inside `onboarding_agreement` → opens `AppPrivacyConfig.PRIVACY_POLICY_URL` in-app; closing returns to privacy page | medium |
| privacy_connect_instance_and_back | scroll to the Connect link; Server config opens; back returns with crash reports still ON | low |
| privacy_change_later_in_settings_privacy | Settings → Privacy toggles the same stored consent (FR-SET-PRIV-01, in progress) | medium |
| privacy_expanded_two_pane_layout | ≥ 840dp: illustration start pane; privacy content end pane; bottom bar under the end pane only; content ≤ 1040dp | low |
| intro_clients_brand_mark_every_page | 32dp mark top start on page 1 and, at the same position, on the privacy page (Skip hidden, 48dp row) | low |
| intro_clients_accessibility_labels | headings, page indicator and switch nodes announced correctly; Terms & Conditions and Privacy Policy spans announced as activatable links | medium |

## Known Gaps

| Gap | Why | Rendered as |
|---|---|---|
| Fresh install is not first-time yet | fork `UserData.DEFAULT.firstTimeUser = false`; the seam `security.first_run_onboarding` lives in template PR #316 (3dd68cd9) | closes when `/kmp-project-template-sync --dev 3dd68cd9` lands (docs.yaml#implementation_preconditions) |
| RootNav still maps ShowOnboarding → sign-in | `RootNavScreen` + `rootTargetRoute` predate onboarding | re-point to `OnboardingRoute` in the fork `RootNavScreen`; upstream seam queued (`rootnav-onboarding-destination-seam`) |
| Settings → Privacy sheet | FR-SET-PRIV-01 port of template `PrivacySheet` in progress | built in the same pass; backs `settings_later_note` |
| Illustration panel colour | ui.yaml declares `tertiaryContainer` / `secondaryContainer` panels for collections / offline; source `PageIllustration` uses `primaryContainer` for all four | not changed by the 2026-11-05 feedback; reconcile in a later pass |
