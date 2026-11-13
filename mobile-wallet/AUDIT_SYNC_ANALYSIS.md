# Template sync analysis — mifos-x/mobile-wallet (mifos-pay)

Target: kmp-project-template `523e1425` (dev mode — openMF/kmp-project-template#317 head).
Fork anchor: `.template-version` `90ff6da6` (reachable) — 9 template commits to adopt; every file has a real merge base.
Lands on: session branch `session-mobile-wallet-20261112171425807`, PR openMF/mifos-pay#2072.

## A — the fork
- Template remote `template` → openMF/kmp-project-template; the app's own remote untouched.
- The workspace project has no `PROJECT_CONFIG.yaml`, so `kmp-template-remote-setup.sh` cannot record the
  `template:` block. Project-metadata gap; the remote itself is correct.

## B — migration ledger (template-migrations.yaml @ 523e1425)
| migration | blocking | state |
|---|---|---|
| whitelabel-engine-layout | yes | adopted ✅ |
| module-deps-seam | yes | adopted ✅ (MS-1/2/3 = 0) |
| ksp-registration | no | adopted ✅ (KS-1/2 = 0) |
| template-first-ownership | no | adopted ✅ |
| platform-shells-3way | no | adopted ✅ |
| ownership-naming-2026-11 | no | adopted ✅ |
| ios-platform-bridges-seam | yes | adopted ✅ (`viewController(platformBridges:)`) |
| onboarding-root-install | no | adopted ✅ |
| web-cors-block | yes | adopted ✅ (`web_cors` block) |

## C — structural detectors
- coverage reconcile: CL-1 LEAK 0 · CL-2 OVERREACH 476 (carve-outs) · CL-3 0 — every syncing path reachable.
- module scaffold: MS-1/2/3 = 0.
- KSP shells: KS-1/2 = 0.
- pure-sync divergence: PS-2 61 FORK-EDITED · PS-3 226 ORPHAN (rc 1). PS-2 is generated or re-derived content:
  docs pages (refresh), `config/*.kt` (`syncForkConfig`), `module-packages.yaml` stamps, and demo-fenced
  blocks the post-sync demo strip removes again (`core/network/build.gradle.kts`, `DataSyncWorker.kt`).
  `Detekt.kt` and `secrets/LAYOUT.yaml` are held. `KptTheme.kt` differs only in a local name.
- ownership transitions: 0 at risk.

## D — what structure misses
- No fork code found in template-owned paths beyond the held files above.

## E — upstream
- Nothing new to queue.

## F — verdict: READY
