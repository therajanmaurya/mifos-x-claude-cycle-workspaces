# Current Work

**Last Updated**: 2026-11-14
**Active Project**: mifos-x/kmp-project-template (with mifos-x/mobile-wallet as the first sync target)
**Branches**: framework=`session-framework-20261101164623912` · workspace=`session-mifos-x-20261031212222497` · template source=`session-kmp-project-template-20261110192515859` @ `08800762`
**PRs**: template https://github.com/openMF/kmp-project-template/pull/317 (DRAFT, base `dev`) · mifos-pay https://github.com/openMF/mifos-pay/pull/2072 (open)
**written_at**: 2026-11-13T20:42:10Z

---

## Session Resumption

- **Goal**: prove the template's GitHub Actions release deploys end to end BEFORE merging #317, fixing everything inside #317 (and the actionhub chain), then sync the template into mifos-pay (#2072).
- **Blocked on (user)**: merge https://github.com/openMF/mifos-x-actionhub/pull/108 (pins publish-web `v2.0.18`).
- **Next steps after #108 merges**:
  1. Release actionhub `v1.0.76` on #108's merge commit (`gh release create … --generate-notes`, same as v1.0.73–75).
  2. Bump the 8 workflow pins in the template `@v1.0.75` → `@v1.0.76`, commit via `git-session-commit-lite.sh --target mifos-x-kmp-project-template`.
  3. New `openMF` branch `release-check/pr-317-<sha8>` at #317's head (`gh api repos/openMF/kmp-project-template/git/refs`; updating an existing branch is blocked by the org ruleset — always create a new one), dispatch `release-multi-platform.yml` web-only with `web_host=gh-pages`, then confirm https://openmf.github.io/kmp-project-template/ serves the **prod** build (title "Money Toolkit", not "(Demo)") with the Playwright check in the scratchpad (`web-verify.ts`).
  4. Mark #317 ready (`gh pr ready 317`), all 13 checks were green at `f28f7e0a`.
  5. Re-run `/kmp-project-template-sync --target mifos-x/mobile-wallet` against the merged template (prod mode), push to #2072.
- **Resume command**: `/context-start mifos-x/kmp-project-template`

---

## Release verification — where each platform stands

| Platform | Status | Evidence |
|---|---|---|
| Android Firebase | ✅ uploads | run 43485762003, versionCode 301 |
| Android Play internal | ✅ uploads | run 43485762003, versionCode 301 (production serves 213) |
| Web — Cloudflare Pages | ✅ prod build served | https://preview.kmp-project-template.pages.dev (run 43491534901) |
| Web — GitHub Pages | ⚠ deploys, but **demo** build | fixed in publish-web v2.0.18 → needs actionhub #108; live site currently shows the demo build from the preview run |
| Linux prerelease | ✅ | run 43432643075 |
| iOS / macOS TestFlight | ❌ account | Apple: "A required agreement is missing or has expired" — the account holder must accept it in App Store Connect → Business. Not code. |

Android production promotion: production already serves 213 (= internal + beta), so promoting that bundle again fails ("does not add any app bundles"). Ship the new build (301 on Play internal) to production via the workflow (`android_rung: production`) or Play Console.

---

## What #317 now contains (all committed + pushed)

- **Release workflow**: actionhub pins `v1.0.75` (valid runner fallbacks; Ruby 3.3.12 on Apple/Android lanes); listing preflight derives the store listing first (`syncForkConfig` in `pre_fastlane_script` for the `validate-store-listing` jobs); self-hosted `release-multi-platform-local.yml` removed (and `.actrc` self-hosted labels).
- **Version code**: `play_aware_version_code!` in `deployment/_shared/config.rb`, used by Firebase + Play internal lanes: `max(commit count after unshallow, highest code on production/beta/alpha/internal + 1)`; a sample key without `private_key` = no Play access. Test `tests/deployment/version-code-test.sh` (8 cases incl. lane `json_key` definition check).
- **App Store**: lookup failure reports Apple's message, not "app not found".
- **Android manifest**: `cmp-clipboard` removed from `core-base/platform` (its `specialUse` foreground service + boot receiver forced a Play declaration). Fork adds `libs.cmp.clipboard` + `includes(clipboardModule())` itself.
- **Sync engine**: never seeds fork-owned images; self-update stays on the caller's pinned branch; issue/PR forms fork-owned.
- **Speed**: Crashlytics mapping id no longer re-merges resources on debug builds; `core-package-ownership` parses the contract once (46 s → 5 s); canaries run in parallel (124 s → 18 s).
- **Docs**: `version-handling.md` Version Code + `versionFile` sections now describe the real build (the rest of that page is still inaccurate — follow-up).

## Chain releases done this session

| Repo | Version | What |
|---|---|---|
| openMF/mifos-x-actionhub | v1.0.74 (#106) | runner fallbacks valid JSON |
| openMF/mifos-x-actionhub | v1.0.75 (#107) | publish-android v2.0.32 + publish-apple v2.0.27 |
| therajanmaurya/…-publish-android-kmp | v2.0.32 (#26) | setup-ruby v1.338.0 |
| therajanmaurya/…-publish-apple-kmp | v2.0.27 (#21) | setup-ruby v1.338.0 |
| therajanmaurya/…-publish-web-kmp | v2.0.18 (#16) | gh-pages builds the requested flavor; test T42 |
| openMF/mifos-x-actionhub | **#108 open** | pin publish-web v2.0.18 → then v1.0.76 |

## Secrets

- `openMF/kmp-project-template` re-synced from the mifos-x vault (template-only sync, 41/42; `mifos-x-match-cert-bundle` is ~400 KB, over GitHub's 48 KB secret limit, and unused by the template — consider dropping the template from its `used_by`).
- A full vault sync also ran (140 ok / 18 failed across 12 repos) before the scope was narrowed.

## Uncommitted framework changes (commit with the next framework commit)

- `core/scripts/secrets-sync-to-ci.sh` + `secrets-sync-to-ci-script-impl.sh`: `--repo <org/repo>` (script mode only), skips non-target secrets before decrypting.
- `/idea-ci local-actions` + `act-ui-serve.sh` + `act-dispatch.sh` + RULE-CI-LOCAL-ACTIONS-001 + MULTI_PLATFORM_RELEASE_GUIDE: default workflow is now `release-multi-platform.yml`.
- `.claude-runtime/state/TEMPLATE_UPSTREAM_QUEUE.yaml`: queued `mirror-deletes-authored-sections-of-fork-docs-pages`, `jacoco-convention-reads-undefined-catalog-version`.

## mifos-pay (#2072) — synced in dev mode, not final

- Synced to template `33efbbae` (dev mode), pushed `239e66d64`; language picker = 22 locales from the new `workspaces/mifos-x/mobile-wallet/idea-layer/idea-plan.yaml` (uncommitted, workspace repo); 33 seeded template images dropped; build + health green.
- Needs a prod-mode re-sync after #317 merges (brings v1.0.76 pins, versionCode helper, cmp-clipboard removal, local-workflow removal).

## Follow-ups

- Field officer still has `security.md` on `dev`.
- Netlify / Vercel steps in publish-web pass inputs those actions don't declare (broken, unused).
- GitHub Pages has no `/cors` relay → exchange rates 404 there (Cloudflare serves it).
- FRED "Today's Rates" shows a generic error instead of the documented "key not configured" state.
- Remaining publish-* repos still carry `vars.CI_RUNNER_* || 'label'` fallbacks.
