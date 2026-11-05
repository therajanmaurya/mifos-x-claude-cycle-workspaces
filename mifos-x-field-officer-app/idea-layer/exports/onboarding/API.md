<!--
generated_by: /idea-feature-export
generated_at: 2026-11-05T00:50:00Z
feature_id: onboarding
generated_from_feature_version: "1.0"
prior_version: "2026-11-04T18:06:00Z"
sources:
  - screens/onboarding/api.yaml
  - screens/onboarding/data-flow.yaml
  - screens/onboarding/docs.yaml
regen_reason: "2026-11-05 operator decisions A+B: writes section now covers both AllowAll (both=true) and ContinueWithChoices (as-shown) paths; terms_url added to local reads; open-url capability added"
-->

# API — Onboarding

Pre-auth and local-only: no Fineract call, no DTO, no permission. The only I/O is three local preference
writes through `UserDataRepository` into `core/datastore` (multiplatform-settings), done once when the
officer taps either privacy button — **Allow and get started** (saves both consents ON) or **Continue**
(saves consents exactly as the switches show).

## Endpoints (0)

None — `api.yaml#endpoints: []` (navigation + local prefs only).

## Local reads

| id | Source | Value |
|---|---|---|
| privacy_policy_url | `kpt.core.model.config.AppPrivacyConfig.PRIVACY_POLICY_URL` (generated from `app-profile/app.yaml#org.privacy_url`) | `https://mifos-products.pages.dev/mobile/field-officer/privacy/` |
| terms_url | `kpt.core.model.config.AppOrgLinks["terms"]` (generated from `app-profile/app.yaml#org.links.terms`) | `https://mifos-products.pages.dev/mobile/field-officer/terms/` |
| consent_defaults | `AppPrivacyConfig.ANALYTICS_ENABLED_BY_DEFAULT` / `CRASH_REPORTING_ENABLED_BY_DEFAULT` (`app-profile/app.yaml#privacy`) | analytics false · crash reporting false — the switches start OFF regardless; onboarding never pre-ticks consent |

## Local writes (on Allow and get started or Continue, in this order)

Both privacy buttons execute the same three writes in the same order. The difference is the values passed to
the first two calls:

| # | id | Target | Allow and get started | Continue | Applied / read by |
|---|---|---|---|---|---|
| 1 | analytics_consent | `UserDataRepository.setAnalyticsConsent(granted: Boolean)` | `true` | switch value | `PrivacyConsentApplier` — `observeAnalyticsConsent` → `AnalyticsHelper.setCollectionEnabled` + `setConsent` |
| 2 | crash_reporting_consent | `UserDataRepository.setCrashReportingConsent(granted: Boolean)` | `true` | switch value | `PrivacyConsentApplier` — `observeCrashReportingConsent` → `CrashReporter.setCollectionEnabled` |
| 3 | first_time_done | `UserDataRepository.setFirstTimeState(firstTimeState = false)` | `false` | `false` | `RootNavViewModel` — `firstTimeUser` false → `RootNavState.Auth`; written LAST so consent is stored before the root state moves on |

## Failure

Any write throws → `OnboardingError.LocalWriteFailed` (`local_write_failed`): `saving = false`,
`saveFailed = true`, `save_error_snackbar` shows, the privacy page stays with both buttons re-enabled,
and `setFirstTimeState(false)` is not called — nothing partial is treated as done
(data-flow `on_allow_get_started.error_state: privacy` / `on_continue_choices.error_state: privacy`).

## Persistence

`clearUserData` (sign-out) copies the loaded record and resets only session fields, so `firstTimeUser` and
both consents survive sign-out.

## Open-URL (agreement links)

Both links in `agreement_text` open in-app via `UrlLauncher.launchInApp` (core-base/platform, `cmp-open-url`
3.5.34). No write occurs; closing the in-app view returns to the privacy page with switches unchanged.

| id | URL constant | Resolved value |
|---|---|---|
| terms_link | `AppOrgLinks["terms"]` | `https://mifos-products.pages.dev/mobile/field-officer/terms/` |
| privacy_policy_link | `AppPrivacyConfig.PRIVACY_POLICY_URL` | `https://mifos-products.pages.dev/mobile/field-officer/privacy/` |

Error: `NoBrowserAvailable` — `launchInApp` returning false is caught; the privacy page stays as-is with
both switches unchanged.
