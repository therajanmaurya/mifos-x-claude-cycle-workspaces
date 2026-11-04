# Jira audit — KMPPT (board 63) vs openMF/kmp-project-template

- Board: https://mifosforge.jira.com/jira/software/c/projects/KMPPT/boards/63
- Repo: openMF/kmp-project-template @ `dev` a70c6bcb
- JQL: `project = KMPPT AND statusCategory != Done ORDER BY updated DESC`
- Audited: 59 open tickets · 2026-11-04 · `/idea-jira` (read-only; nothing written to Jira)

| Verdict | Count |
|---------|------:|
| DONE-UNCLOSED | 10 |
| PARTIAL | 14 |
| NEEDS-WORK | 12 |
| STALE | 20 |
| UNCLEAR | 3 |

Only 4 of 59 tickets are referenced by any commit, branch or PR (KMPPT-91 #134 closed, KMPPT-88 #99 open, KMPPT-81 #92 open draft, KMPPT-23 #54 closed) — every other verdict rests on reading the code.

## DONE-UNCLOSED — close these

| Key | Summary | Status | Evidence | Next |
|-----|---------|--------|----------|------|
| KMPPT-22 | E2E unit testing suite (KMP + CMP) | To Do | 255 test files across commonTest/desktopTest/nativeTest/androidInstrumentedTest, 41 ViewModel tests; Turbine `libs.versions.toml:248`, Kover `:82`; CI runs tests + kover (`quality-gate.yml:126-130`) | Close |
| KMPPT-28 | Encrypt datastore data (AES-256) | On Deck | AES-256-GCM `expect class FieldEncryptor` (`core-base/crypto/.../FieldEncryptor.kt:13-19`) + `SecureKeyProvider`; `SecureStoreCore.kt:113` encrypts, used by `UserPreferencesRepositoryImpl.kt:34`; tests `SecureStoreCoreTest.kt`, `WebSecureCryptoTest.kt` | Close |
| KMPPT-30 | Database base for web source set | To Do | `core-base/database/src/jsMain/.../AppDatabaseFactory.kt` (WebWorkerSQLiteDriver + OPFS) + wasmJs actual + `PlatformDatabaseModule.{js,wasmJs}.kt`; `WebInvalidationProbeTest.kt` | Close |
| KMPPT-32 | Cross-platform app icon + branding | On Deck | Icons on every platform: `cmp-android/.../mipmap-*`, `splash.xml`, `AppIcon.appiconset`, `cmp-desktop/icons/ic_launcher.{ico,icns}`, `app-profile/icons/web-favicon.ico` | Confirm design handoff, close |
| KMPPT-45 | Product flavours in KMP | In Progress | `KMPFlavorsConventionPlugin.kt:118-160` (demo/prod × debug/staging/release) → BuildConfig; doc `cross-cutting/flavors-extension.md`; CI `flavor` input (`release-multi-platform.yml:136`); PRs #141 #231 | Close (naming differs from dev/staging/prod) |
| KMPPT-47 | compileSdk 36, AGP, Gradle, deps | On Deck | compileSdk 37 (`libs.versions.toml:16`) read by `KotlinAndroid.kt:30` + `KMPLibraryConventionPlugin.kt:56`; AGP 9.4.0; Gradle 9.7.1 | Close |
| KMPPT-78 | Version catalog to latest stable + JDK 21 | In Progress | `jvmToolchain=21` (`:20`), Kotlin 2.4.20, KSP 2.3.11, Ktorfit 2.7.5, kotlinx-datetime 0.8.0; the named analytics files no longer exist | Close (CI setup-java still 17, `quality-gate.yml:91`) |
| KMPPT-90 | Kotlin 2.3 / AGP 8.13 / android-KMP library plugin | On Deck | Kotlin 2.4.20, AGP 9.4.0; `KMPLibraryConventionPlugin.kt:30` applies `com.android.kotlin.multiplatform.library`, host tests (`:94`) + android resources (`:102`) enabled; PR #185 | Close |
| KMPPT-2 | Release on Google Play via GitHub Actions | On Deck | `release-multi-platform.yml` Play stages; run 29199448936 passed "Stage 1 — Play Internal"; release 2026.7.16 carries the prod `.aab` | Close |
| KMPPT-34 | Publish Android Demo/Prod to Firebase | On Deck | `deployment/_shared/project_config.rb:148-150` prod + demo Firebase app ids (`release-multi-platform.yml:371-372`); Firebase stage succeeded in run 29199448936 | Close |

## PARTIAL — finish or re-scope

| Key | Summary | Status | Met / not met | Next |
|-----|---------|--------|---------------|------|
| KMPPT-51 | Generic error UI in design system | In Progress | Met: Lottie default + fallback (`DefaultLottieAnimations.kt:38`), overrides (`ScreenStateDefaults.kt:61-232`), server message (`:125`). Not: 404/502/airplane-mode screens; 401 reuses generic (`ScreenContent.kt:114`) | Add per-category visuals |
| KMPPT-42 | Multi-language support | In Progress | 19 locales in `core-base/ui/.../composeResources`; only Hindi among Indian languages | Add Indian locales or close as covered |
| KMPPT-23 | E2E UI testing (common + platform) | In Review | Met: ~20 commonTest Compose UI tests + Android instrumented tests. Not: CI runs only `koverXmlReport`; no instrumented/iOS UI runs, no screenshots | Add instrumented + iOS UI CI jobs |
| KMPPT-37 | Unit tests for database | On Deck | Met: TypeConverter tests in `core/database`. Not: 0 tests in `core-base/database` (AppDatabaseFactory) | Add AppDatabaseFactory tests |
| KMPPT-79 | Cross-OS Fastlane setup script | In Progress | Met: Firebase lane runs unattended (run 29199448936), docs in BOOTSTRAP.md. Not: no PowerShell / cross-OS script, no per-OS proof | Add scripts or narrow scope |
| KMPPT-21 | Desktop deploy macOS/Windows/Ubuntu | To Do | Met: .deb + .pkg reach release 2026.7.16 via `release-multi-platform.yml`. Not: Windows rung skipped in every recent run, no .msi/.exe asset | Run a green Windows rung |
| KMPPT-64 | Sync: repository management core | To Do | Met in bash: upstream URL, `--template-ref`, sync branch, FORK_STATE (`sync-dirs.sh:82-300`). Not: protocol switching, retry, multi-upstream | Close with epic or re-scope |
| KMPPT-65 | Sync: selective engine | To Do | Met: contract include/exclude, fork-file preservation, 3-way merge, `--dry-run`/`--only`. Not: incremental mode, symlink/permission handling | Close with epic |
| KMPPT-66 | Sync: conflict resolution | To Do | Met: catalog-3way + include-union merges, per-file strategy, `--post-sync`. Not: categorization, confidence, reports, rollback | Close with epic |
| KMPPT-67 | Sync: advanced patterns | To Do | Met: `--only`, weekly cron (`sync-dirs.yaml`). Not: multi-directional, federation, hooks | Close as out of scope |
| KMPPT-69 | Sync: testing framework | To Do | 14 bash tests in `tests/customization-surface/` + pbxproj canary; no workflow runs them | Add a CI job for them |
| KMPPT-5 | Sync + auto PRs to child repos | On Deck | Met: optimized sync, PR via `create-pull-request` (`sync-dirs.yaml:397`), docs `template-sync.md`. Not: pull-per-fork, no CHILD_REPOS push | Decide pull vs push; close or re-scope |
| KMPPT-31 | Create new project from template | To Do | `is_template: true`, `fork-init.sh`, `fork-quickstart.md:21`; the "Use this template" step isn't documented | Add that step, close |
| KMPPT-29 | Automate GitHub secrets verify + create | To Do | `scripts/secrets/sync-secrets-to-github.sh` pushes via `gh secret set`; no existence check, no `--org` | Add check + org support, or accept |

## NEEDS-WORK

| Key | Summary | Status | Evidence | Next |
|-----|---------|--------|----------|------|
| KMPPT-50 | @DevicePreviews with @PreviewParameter | On Deck | `git grep DevicePreviews\|@PreviewParameter` → none | Add multipreview annotation |
| KMPPT-88 | Empty onboarding screens | In Review | `RootNavScreen.kt:104` `//onboardingDestination()`; no `feature/onboarding`; PR #99 open on old `org.mifos` packages | Rebase #99 to `kpt.*` or redo |
| KMPPT-87 | Time-based theming | In Review | `DarkThemeConfig` = FOLLOW_SYSTEM/LIGHT/DARK only; no schedule code | Add a scheduled theme option |
| KMPPT-7 | Publish build-logic to Gradle Plugin Portal | To Do | `includeBuild("build-logic")` (`settings.gradle.kts:49`); no plugin-publish config | Decide if still wanted |
| KMPPT-52 | Epic: keystore management → Gradle DSL | To Do | `keystore-manager.sh` moved, still bash (`deployment/_shared/scripts/`, #307); no Gradle tasks | Confirm Gradle migration is wanted, else close |
| KMPPT-58 | GitHub secrets via API (no gh CLI) | On Deck | `keystore-manager.sh:1790-1994` + `sync-secrets-to-github.sh:117` use `gh secret` | Blocked on KMPPT-52 decision |
| KMPPT-59 | CLI + task orchestration | To Do | Commands are bash branches (`keystore-manager.sh:2101+`) | Blocked on KMPPT-52 |
| KMPPT-60 | Testing framework (keystore tasks) | To Do | No keystore/secrets tests | After Gradle tasks exist |
| KMPPT-61 | Docs + migration guide | To Do | Docs cover the bash tooling only | After Gradle tasks exist |
| KMPPT-62 | Backward compatibility wrapper | To Do | Nothing migrated, so nothing to wrap | After Gradle tasks exist, or close with epic |
| KMPPT-68 | Sync monitoring + diagnostics | To Do | No progress/metrics/alerting in sync | Close as out of scope, or a summary report |
| KMPPT-93 | Rename `dev` → `development` | Done | Closed 2026-11-04 on maintainer confirmation. At close GitHub still reported default `dev` (`development` 143 behind); `sync-dirs.yaml` references `dev` | Update `sync-dirs.yaml` if the GitHub switch is still pending |

## STALE — close as superseded

| Key | Summary | Why |
|-----|---------|-----|
| KMPPT-70 | Epic: customizer.sh → Gradle plugin | customizer.sh became a shim to `fork-init.sh` (#286); customization = `app-profile/` + `syncForkConfig` (`SyncForkConfigPlugin.kt:64`) |
| KMPPT-71 | Project template management | Replaced by `customization-surface.yaml` + `app-profile/` |
| KMPPT-72 | Package/namespace transformation | `app-profile/package-ledger.yaml` + package registry codegen (#300) |
| KMPPT-73 | Content/resource transformation | `syncForkConfig` writes names/branding/store text from `app.yaml` |
| KMPPT-74 | Build system configuration | `syncForkConfig` regenerates `gradle/fork.properties` |
| KMPPT-75 | Validation + QA | `doctor.sh`, `scripts/product-health/checks/*`, `syncForkConfig --check` |
| KMPPT-76 | Interactive setup | `setup-project.sh` / `fork-init.sh` + declarative `app-profile/` |
| KMPPT-77 | Project migration | `template-migrations.yaml` + `migration-ledger.yaml` + `sync-dirs.sh` (#286, #293) |
| KMPPT-63 | Epic: sync-dirs.sh → Gradle sync | Built as the contract-driven bash engine instead (#286, #313, #315); its children are PARTIAL above |
| KMPPT-80 | Epic: Dokka/Docusaurus docs | Replaced by `scripts/docs/` + `docs/architecture/` + Docsify + docs-refresh/check workflows (#309); no Dokka anywhere |
| KMPPT-81 | docs-generator/ structure | Never on dev; only in open draft PR #92 — close #92 too |
| KMPPT-82 | Dokka convention plugin | Only in draft #92; KDoc handled by `api-docs-gen.sh` |
| KMPPT-83 | customizer.sh docs setup | customizer.sh gone; docs workflows ship in-repo |
| KMPPT-84 | Push docs to Docusaurus repo | Docs live in-repo; `docs-refresh.yml` PRs drift |
| KMPPT-85 | Docs CI/CD workflows | `docs-refresh.yml` + `docs-check.yml` replace them |
| KMPPT-86 | Docs validation + training | Pipeline never built; current docs are onboarding/troubleshooting/architecture |
| KMPPT-91 | Integrate SQLDelight | PR #134 closed unmerged; repo standardized on Room |
| KMPPT-20 | Tests for composite actions | No `.github/actions/`; workflows call `openMF/mifos-x-actionhub` — move the ticket there |
| KMPPT-27 | Maven Central library publishing | App template, not a library; misfiled |
| KMPPT-43 | Document from repository (PocketFlow) | Superseded by the `docs/architecture` pipeline |

## UNCLEAR — needs grooming

| Key | Summary | Why |
|-----|---------|-----|
| KMPPT-38 | App encryption documentation | Description is only an image; no checkable criteria |
| KMPPT-94 | EPIC-01 | Empty epic, no description, no children |
| KMPPT-6 | Run fork GitHub Actions in another org publicly | Summary only, no criteria |
