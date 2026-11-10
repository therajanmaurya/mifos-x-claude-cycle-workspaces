# Sync analysis — mifos-x/mobile-wallet (openMF/mifos-pay) ⟵ kmp-project-template @ 90ff6da6 (dev mode)

`/kmp-project-template-sync --target mifos-x/mobile-wallet --dev 90ff6da6671d` STEP 0.ANALYZE, 2026-11-06, run in its
declared position (after STEP 0.5, before STEP 1). Template ref = head of template PR #316 (unmerged).

## A — the fork

- Previous session branch `session-mobile-wallet-20260819181213704` was SPENT (its PR openMF/mifos-pay#2064 merged
  2026-09-21). STEP 0.5 cut a fresh `session-mobile-wallet-20261106011512` from `upstream/dev` (b722bdbfe).
  The spent branch still carries one post-merge commit (`99681f61d`, 2026-11-05, deletes 4 tester flow pairs + 1
  AGENT_AWARENESS row) that is not in this sync; it stays on `origin/session-mobile-wallet-20260819181213704`.
- Anchor `.template-version#template_sha` = `6fe88bad` (2026-08-19), reachable and an ancestor of 90ff6da6:
  **48 template commits** land in this run. A real per-file merge base exists.

## B — adoption plan (template-migrations.yaml @ 90ff6da6)

| migration | state |
|---|---|
| whitelabel-engine-layout | adopted |
| module-deps-seam | adopted (MS-1=0 MS-2=0 MS-3=0) |
| ksp-registration | detect said adopted (KS-1=0 KS-2=0) but was NOT: hand-written AppDatabase/AppStoreRegistry/StoreModule (16 stores) — converted in-branch at STEP 4 (detector defect enqueued) |
| template-first-ownership | adopted |
| platform-shells-3way | detector reports 80 hardening/upstream (re-measured at STEP 3.25) |
| ownership-naming-2026-11 | adopted (no ProjectStoreModule.kt); words/files rows applied by the engine |
| ios-platform-bridges-seam | adopted (ViewController.kt has no storeKit2Bridge param) |
| onboarding-root-install | adopted by detect (fork has no feature/onboarding, no fork install); template's module arrives |

## C — structural detectors

| detector | rc | verdict |
|---|---|---|
| sync-coverage-reconcile (template) | 0 | CL-1 LEAK 0 · CL-2 476 (fork carve-outs) · CL-3 0 |
| sync-module-scaffold-audit | 0 | MS-1/2/3 = 0 |
| sync-ksp-shell-audit | 0 | KS-1/2 = 0 |
| sync-puresync-divergence | 1 | PS-1 525 behind · **PS-2 34 fork-edited** · PS-3 432 orphan |
| sync-ownership-transition (fork HEAD contract) | 1 | hardening/upstream 80 — every one has ZERO fork delta (23 == template, 56 == base) except Detekt.kt (+1 line); hardening/fork-only 15 → decided at STEP 3.6 |

## D — what the detectors cannot see (ranked by what would be destroyed)

`kmp-template-ownership-audit.sh` @ 90ff6da6: **156 template-owned + authored rows** that `--mirror`/overlay would
remove or overwrite. The ones that matter:

1. **The app shell.** mifos-pay's real UI root is `org.mifospay.shared.*` in `cmp-shared/src/commonMain` (MifosApp,
   MifosNavHost, MifosPayViewModel, InstanceSelector, Koin `featureModules`/`sharedModule` — 17 files + 2 iOS view
   controllers). `cmp-shared/**` is template-owned, so the strict mirror would DELETE the app. Bridged through
   fork edits to template files: `cmp-navigation` `ComposeApp.kt` (+153 vs base), `AppViewModel.kt` (+186),
   `cmp-navigation/security/*` (AppLock / Unauthorized / PlatformAuthenticator gates), `instance/InstanceSelectorRoute.kt`,
   and `cmp-shared/.../utils/KoinExt.kt` (splices the fork Koin modules in). A full-copy of KoinExt alone gives a
   GREEN build whose ~60 feature ViewModels fail to resolve at runtime.
2. **Fork code inside core-base**: `core-base/network` org.mifos.corebase.network (12 files, used by core/network and
   libs/mifos-loans), `core-base/platform` PlatformBuildConfig expect/actual (6, used by feature/auth), two
   `template.core.base.*` compatibility shims (used by cmp-shared, feature/auth, feature/passcode,
   feature/transfer-intrabank, libs/mifos-loans).
3. **Platform files**: `cmp-android/.../org/mifospay/MifosPayApp.kt`, desktop `main.kt` + entitlements plists,
   iOS `GoogleService-Info.plist` + `cmp-ios.xcscheme` (+2 committed xcuserdata files — junk).
4. **Dead modules**: `core/analytics` (fork, 21 files) and `core-base/analytics` (template-removed) — included in
   settings.gradle.kts but depended on by nothing.
5. **settings.gradle.kts** carries ~30 fork includes (include-union keeps them; RULE-KMP-FORK-MODULE-SEAM-001 wants
   them in settings.local.gradle.kts).
6. Identity / derived files the template now renders from app-profile: deployment/*, secrets/LAYOUT.yaml,
   module-packages.yaml, docs/images/graphs*.

## E — upstream direction

Enqueued as each step surfaces them (TEMPLATE_UPSTREAM_QUEUE.yaml). Leading candidates: a fork-owned commonMain
package in cmp-shared (the reason mifos-pay's shell lives in a template-owned root), PlatformBuildConfig as a
core-base/platform primitive, fork-owned `.github/CONTRIBUTING.md` / fork workflows / detekt baseline / fork docs.
Framework (not template) defect healed in this run: `git-session-start-target-lite.sh` reused a spent session branch.

## F — verdict

`READY-WITH-MIGRATION` — nothing is destroyed if STEP 3.6 decides all 156 authored rows before STEP 4 (the app shell
is HELD, core-base fork code MOVED/held, shims migrated, dead modules dropped). Proven by the STEP 4.7 compile and
the Koin simple-name collision test.
