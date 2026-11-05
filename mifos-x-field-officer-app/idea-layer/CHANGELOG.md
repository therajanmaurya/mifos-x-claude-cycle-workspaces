# Idea Evolution Log — mifos-x-field-officer-app

## 2026-03-22 — idea-layer generated from existing project
- **What**: Reverse-engineered from PROJECT.md, FEATURES_INDEX, SPEC files
- **Source**: /project-migration v2.86.5
- **Features**: 20 discovered
- [design-system-stitch] 2026-10-02 — DESIGN.md uploaded to Stitch (asset_id=9551377288795375599, design_md_sha=c1e7dbe50f77)

## 2026-11-05 — signin consent line: Terms & Conditions + Privacy Policy links (/idea-plan-add enhance signin)
- **What**: The pinned bottom-bar consent line now reads "By signing in you accept our Terms & Conditions and Privacy Policy." (was "By signing in you agree to our Terms of Service and Privacy Policy." as plain text). "Terms & Conditions" → AppOrgLinks["terms"] (https://mifos-products.pages.dev/mobile/field-officer/terms/) and "Privacy Policy" → AppPrivacyConfig.PRIVACY_POLICY_URL are inline in-app links (LinkAnnotation → LocalUrlLauncher.launchInApp). testTag signin:consent unchanged; the links are screen-level effects, not ViewModel actions.
- **Why**: Operator instruction 2026-11-05, implemented in source (feature/signin/.../ui/SignInScreen.kt ConsentText) and verified on device. Signing in is the acceptance act — the same accept-by-continuing rule as the onboarding agreement line; the document is named as published ("Terms & Conditions").
- **Requirements**: FR-001a added.
- **Docset**: screens/signin/ui.yaml (consent_text: literal copy, args, terms_link + privacy_policy_link with action contracts) + flow.yaml (open_terms / open_privacy_policy transitions); docs/tests regenerated (screen_actions, decision consent-accept-by-continuing, +2 test scenarios); _strings +screens.signin.{consent,terms,privacy_policy}; 8 signin Stitch renders regenerated.

## 2026-11-05 — onboarding design: fixed bottom action bar, shared-axis page transition, 32dp mark (/idea-plan-add enhance onboarding)
- **What**: (1) Page content changes with the template shared-axis-X motion (core-base/ui KptSharedAxis: forward when advancing, back when going back; MaterialTheme.motion.durationLong1, 450ms); the top row and the bottom bar do not slide, and the bar's buttons crossfade (durationMedium1, 250ms) when the privacy page swaps Next for the two finishing buttons. (2) On every page the page dots + primary action(s) are pinned in a FIXED bottom bar — intro: centred dots + full-width Next; privacy: centred dots, then the save-failed error text when shown, then full-width filled "Allow and get started" and full-width outlined "Continue without sharing" / "Continue with my choices". Only the content above scrolls; on privacy that is title, lead, both switch rows, the no-client-data note, the agreement line (moved up out of the bar), "You can change this later in Settings.", then "Connect to your Mifos instance". On expanded (≥840dp) the bar sits under the end (text) pane. (3) The Mifos X mark is 32dp (not 48dp) and shows on every page, privacy included; the top row keeps a 48dp minimum height so the mark doesn't jump where Skip is hidden. The save error is inline text in the bar (save_error_snackbar / onboarding_save_error → save_failed_text / onboarding_save_failed).
- **Why**: Operator direct design feedback 2026-11-05, already implemented in source (feature/onboarding/.../ui/OnboardingScreen.kt) and verified on a physical device; this entry brings the idea-layer in line so idea-layer and source don't drift.
- **Requirements**: FR-ONB-02 + FR-ONB-07 revised; FR-ONB-08 added (fixed bottom action bar + shared-axis transition).
- **Docset**: screens/onboarding/ui.yaml (state layouts → column_with_bottom_bar, layout.regions, new motion block, brand_mark on all 4 states, save_failed_text, agreement_text moved to the scrolling content) + flow.yaml + maestro/happy_path.yaml (no scroll needed for the finishing buttons; brand mark asserted on privacy); journeys/field-officer-first-run.yaml (connect-instance branch scrolls; save-failed tag); IDEA_CORE (+FR-ONB-08, +brand_mark, +save_failed_text). docs/tests regenerated through /idea-feature-enrich; all 4 Stitch mockups + 4 previews regenerated; SPEC re-exported. No strings changed.

## 2026-11-05 — onboarding privacy page: "Allow / Continue without" + Terms (/idea-plan-add enhance onboarding)
- **What**: The single "Get started" on the privacy page becomes two equally visible buttons. **Allow and get started** (primary) turns both consents ON, saves analytics=true and crashReports=true, then setFirstTimeState(false) LAST and opens sign-in. **Continue without sharing / Continue with my choices** (outlined, same size; label follows the switches) saves them exactly as shown, then setFirstTimeState(false). Both switches still start OFF and stay visible. An agreement line above the buttons — "By using our service you accept our Terms & Conditions and Privacy Policy." (operator copy) — links both in-app: Terms & Conditions → AppOrgLinks["terms"] (https://mifos-products.pages.dev/mobile/field-officer/terms/), Privacy Policy → AppPrivacyConfig.PRIVACY_POLICY_URL. It is one Text tagged onboarding_agreement with inline link spans tapped by their text; the standalone privacy policy link and its onboarding_privacy_policy tag are retired. Privacy lead reworded.
- **Why**: Operator decisions 2026-11-05 — A "Allow / Continue without", chosen after being told pre-ticked / opt-out consent is invalid under GDPR + ePrivacy, UK GDPR / PECR and India DPDP s.6 (consent must be an affirmative act and declining as easy as accepting); B "Create + publish Terms" — Terms page published and verified live ("Terms & Conditions — Field Officer App").
- **Requirements**: FR-ONB-03, FR-ONB-04 revised; FR-ONB-07 added (agreement line).
- **Docset**: screens/onboarding/{ui,flow}.yaml + maestro/happy_path.yaml; strings +allow_get_started, +continue_without, +continue_choices, +agreement ("By using our service you accept our %1$s and %2$s."), +terms ("Terms & Conditions"), −get_started, privacy_lead + privacy_policy ("Privacy Policy") reworded; IDEA_CORE screen.onboarding edges (−get_started, −privacy_policy_link, +agreement_text, +allow_get_started, +continue_choices). docs/tests regenerated through /idea-feature-enrich; privacy mockup regenerated through /idea-feature-stitch.

## 2026-11-04 — onboarding added (/idea-plan-add add-feature onboarding)
- **What**: First-run onboarding, shown once on a fresh install before sign-in: three intro pages (clients/groups/centres in the field · repayments and collection sheets · offline and sync later) with Skip, Next, page indicator and back, then a privacy page — Share usage analytics and Send crash reports, both OFF by default, plain explanation, hosted privacy policy link, "change this later in Settings". Get started saves both choices and setFirstTimeState(false), then opens sign-in. Optional "Connect to your Mifos instance" → serverConfig.
- **Why**: Operator decision 2026-11-04 — "analytics off until consent; onboarding is the place to ask". Prod builds start Analytics + Crashlytics collection OFF and no screen asked for consent. Resolves signin's deferred `onboarding` candidate.
- **Requirements**: FR-ONB-01..06, NFR-ONB-01; follow-up FR-SET-PRIV-01 (Settings privacy toggles).
- **Docset**: screens/onboarding/{docs,ui,api,flow,data-flow,demo-data,tests}.yaml + maestro/happy_path.yaml; 23 strings under screens.onboarding.*; flows/authentication.yaml + screens/signin/{ui,flow}.yaml re-pointed (ShowOnboarding → onboarding → signin); IDEA_CORE.yaml started.
- **Source findings (not fixed here)**: UserData.DEFAULT.firstTimeUser is false, so a fresh install never reaches ShowOnboarding today; RootNavScreen maps ShowOnboarding → sign-in.

## 2026-10-27 — profile designed (/idea-plan-add --rebind profile)
- **What**: The signed-in officer's account, opened from the Home avatar: full name, username, Loan officer / Staff chip, office, roles; what Home shows (my portfolio vs office); the live server instance, URL and tenant; Change password (server refusal shown verbatim, re-sign-in on success); Sign out (the Settings dialog). Detail shell with a back arrow; offline shows the identity saved at sign-in.
- **Why**: The navigation drawer was removed and its header was the only way to Profile; the existing screen was three lines with no app bar.
- **Requirements**: FR-PRO-01..06, SFR-031..032, NFR-PRO-01.
- **Docset**: screens/profile/{docs,ui,api,flow,data-flow,demo-data,tests}.yaml + maestro/happy_path.yaml; 27 strings under screens.profile.*.
- **Gateway (measured)**: POST users/{id}/pwd routes and validates (policy 12–50 chars, upper/lower/digit/symbol; server-side repeat match); fieldofficer = Irving Zepeda, no staff link, role OFICIAL DE CAMPO. Probes used mismatched pairs — no password changed.

## 2026-10-27 — offlineSync added (/idea-plan-add)
- **What**: Settings → Offline sync, a separate feature from Sync & Drafts. The officer selects existing centres / groups / clients; a background job (sync/) downloads each one's full downstream tree — groups, clients, every loan and savings account (closed included), addresses, identifiers, notes, charges, documents with file contents, datatables, templates — through the screens' own stores; offline loan repayments and savings transactions upload as soon as online. Live dashboard from durable job state; Manual or Automatic refresh (interval, Wi-Fi only, while charging).
- **Why**: Field officers work without signal; the v1 drawer "Offline Sync" was never ported, and offline repayments were queued with nothing to send them.
- **Source**: Operator decisions 2026-10-27; redesign of 6b66e8a43 feature/offline (dashboard + 5 sync screens).
- **Requirements**: FR-OFF-01..08, SFR-029..032, NFR-OFF-01.
- **Docset**: screens/offlineSync/{docs,ui,api,flow,data-flow,demo-data,tests}.yaml + maestro/happy_path.yaml.

## 2026-10-26 — home dashboard added (/idea-plan-add)
- **What**: Permission-aware field officer home dashboard — today's collections, work queue, meetings today, portfolio at a glance, quick actions, recent records. Becomes the Home tab body; search stays on the top-bar icon.
- **Why**: A field officer's first screen should be the day's work; the original Home was search only.
- **Source**: Fineract API + permission audit (sandbox 1.17.0-SNAPSHOT: 603 paths, 710 permission codes) and the gateway field officer role.
- **Decisions**: staff-linked "my portfolio" with office-wide fallback · own-loan approval/disbursal queues · dashboard IS Home.
- **Requirements**: FR-DASH-01..07, SFR-024..028, NFR-PERM-01.
- **Docset**: screens/home/{docs,ui,api,flow,data-flow,demo-data,tests}.yaml + maestro/happy_path.yaml.
- **Rename**: feature id `home` (operator: "keep the name clean"); the previous `home` plan row — the search surface — is now `search`.
