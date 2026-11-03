# Sync analysis — mifos-x-field-officer-app ⟵ kmp-project-template @ 0bbb4bed (dev mode)

`/kmp-project-template-sync` STEP 0.ANALYZE, 2026-11-03. Converged at `0bbb4bed` (gate: CONVERGED (DEV)).

## A — the fork

- Branch `session-mifos-x-field-officer-app-20261028144044988` (PR openMF/mifos-x-field-officer-app#2706), head `ea9803a23`.
- Anchor `.template-version#template_sha` = `0bbb4bed`, reachable; the per-file merge base exists.

## B — adoption plan (template-migrations.yaml)

| migration | state |
|---|---|
| whitelabel-engine-layout | adopted |
| module-deps-seam | adopted (detector C) |
| ksp-registration | adopted (detector C) |
| template-first-ownership | adopted |
| platform-shells-3way | adopted (detector C) |
| ownership-naming-2026-11 | adopted |

## C — structural detectors

| detector | rc | verdict |
|---|---|---|
| sync-coverage-reconcile | 0 | every contract-synced path reachable |
| sync-module-scaffold-audit | 0 | every module carries its seam |
| sync-ksp-shell-audit | 0 | no fork content in a KSP shell |
| sync-puresync-divergence | 1 | 21 PS-2 rows, all held or re-derived (below); 5 PS-3 orphans, all held |
| sync-ownership-transition | 0 | no fork content at risk |

The 21 PS-2 rows:
- **held (3)**: `.github/workflows/cla-check.yml` (never-touch), `cmp-navigation/.../utils/RootUtils.kt`, `cmp-shared/README.md`.
- **re-derived by the post-sync steps (17)**:
  - 7 `core/*/module-packages.yaml` (remove-demo);
  - demo-stripped: `sync/.../DataSyncWorker.kt`, `core/network/build.gradle.kts` and 2 `WebInvalidationProbeTest.kt`;
  - 6 `App*` config regions (syncForkConfig).
- **re-derived by fork-init (1)**: `secrets/LAYOUT.yaml`.

## D — what the detectors cannot see

- The surface report over all 59 synced roots shows AT-RISK as exactly the 18 re-derived files above.
- **Fork fixes applied in this run** (`e3c947a56`):
  - `icon/KptIcons.kt` → `ForkIcons.kt` and `icon/DesignIcons.kt` → `ForkDesignIcons.kt`. `icon/` is a template package, so a fork's own glyph files take the `Fork*` name. The files now carry KDoc, so Detekt is clean.
  - The duplicate `Contributing.md` index entry was dropped. It had the same blob as `CONTRIBUTING.md`, and only one of the two can exist on a case-insensitive disk.
- `app-profile` is schema-current. The one template key absent here is `network.demo_base_url`, which this fork removed on purpose (documented in `app.yaml`).

## E — upstream

Fixed in the template during this run (dev mode):

| commit | fix |
|---|---|
| bd04d4d8 | `icon/**` is template-owned again (`AppIcons.kt` merge, `Fork*` fork). Narrowing the icon row had broken MP-1. |
| 55968599 / 579ea54a | `doctor.sh`: freshness checks only the keys `derive.rb` owns; template currency uses the `template` remote (no tags) and the recorded `template_sha`. |
| 088195c4 | `strings-union` keeps the fork's string order, so an untouched `strings.xml` no longer churns on every sync (test SU-1..3). |
| 0bbb4bed | `gen-kotlin-filelist.sh` sorts with `LC_ALL=C`, so the Xcode file list no longer depends on the machine locale. |

Fixed in the framework: `kmp-template-surface-report.sh` reported a false "nothing at risk" when `--roots` was padded. A canary leg (S-6) now covers it.

Outside the sync: openMF/mifos-x-field-officer-app carries the prerelease tag `2026.10.1-beta.0.8` on a PR-branch commit that descends from the `2026.11.0` release commit. Any clone that fetches tags fails reckon's version calculation.

## F — verdict

**CONVERGED (DEV) @ 0bbb4bed.**
- Every required step is green in the ledger.
- `assembleProdDebug` passes.
- product-health is 40/0/0.
- syncForkConfig is idempotent.

Merge template PR #315, retrain, then re-run in prod mode before #2706 is marked ready.
