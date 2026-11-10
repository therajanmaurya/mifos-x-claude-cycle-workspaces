# Sync analysis — mifos-x-field-officer-app ⟵ kmp-project-template @ 90ff6da6 (dev mode)

`/kmp-project-template-sync` STEP 0.ANALYZE, 2026-11-05, run in its declared position (after STEP 0.5, before STEP 1).
Template ref `90ff6da6671d` = head of template PR #316 (unmerged), carrying the fixes for the defects the
32f6a6ce iteration enqueued. The 32f6a6ce apply was discarded (restored to session HEAD `adaa42290`, no stash).

## A — the fork

- Branch `session-mifos-x-field-officer-app-20261103235023611` (draft PR openMF/mifos-x-field-officer-app#2707).
- Anchor `.template-version#template_sha` = `a70c6bcb`, reachable; per-file merge base exists.

## B — adoption plan (template-migrations.yaml)

| migration | state |
|---|---|
| whitelabel-engine-layout | adopted |
| module-deps-seam | adopted (MS-1=0 MS-2=0 MS-3=0) |
| ksp-registration | adopted (KS-1=0 KS-2=0) |
| template-first-ownership | adopted |
| platform-shells-3way | adopted (detector C) |
| ownership-naming-2026-11 | adopted |
| ios-platform-bridges-seam | adopted |
| onboarding-root-install (new) | **NOT ADOPTED** — `blocking: false`, applied inside the sync branch after the merge, before the build (move the install into RootNavScreen with the fork's callback, delete the AuthNavigation install, drop the settings.local include + feature-deps edge) |

## C — structural detectors

| detector | rc | verdict |
|---|---|---|
| sync-coverage-reconcile (template) | 0 | CL-1 LEAK 0 (was 2 at 32f6a6ce) |
| sync-module-scaffold-audit | 0 | every module carries its seam |
| sync-ksp-shell-audit | 0 | no fork content in a KSP shell |
| sync-puresync-divergence | 1 | 58 PS-2 + 25 PS-3; held, re-derived or historic (decided at STEP 3.6) |
| sync-ownership-transition | 0 | no fork content at risk (re-run at STEP 3.25 with the pre-sync contract snapshot) |

Nothing destructive. The only structural pre-work is the in-branch onboarding migration.

## D — what the detectors cannot see

- The onboarding double-install: compiles only once RootNavScreen passes the fork's callback; a missed AuthNavigation
  removal crashes the nav graph at runtime with a clean build.
- `feature/home` strings carry `%%` (fork-owned copy of the old template home); the template fixed its own copy and the
  new `compose-strings-apostrophe` CS-2 check fails the fork until it is fixed in the fork.

## E — upstream direction

Defects from the 32f6a6ce iteration are fixed at 90ff6da6. New findings are enqueued in `TEMPLATE_UPSTREAM_QUEUE.yaml`
as the steps surface them.

## F — verdict

`READY-WITH-MIGRATION` — no blocking pre-work; onboarding-root-install is applied in-branch at STEP 4 and proven by
the STEP 4.7 compile.
