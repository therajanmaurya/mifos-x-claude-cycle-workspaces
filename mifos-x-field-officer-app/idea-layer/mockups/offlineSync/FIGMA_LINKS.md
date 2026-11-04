# FIGMA_LINKS.md — offlineSync

<!-- schema: v3.2 | generated: 2026-11-04T10:36:48.967Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [10780096558615730514](https://stitch.google.com/projects/10780096558615730514) |
| Design System ID | 9551377288795375599 |
| Generated | 2026-11-04T10:36:48.736Z |
| Success | 6/6 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | 73edb4992ae344d49117d7d63cbe787f | 01-offlineSync-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | 47d285f3095b482b8f430ca05993803c | 02-offlineSync-content | PNG ✅ | HTML ✅ | ✅ generated |
| syncing | d65b7747606b49659adb692be3953d11 | 03-offlineSync-syncing | PNG ✅ | HTML ✅ | ✅ generated |
| partial_failure | d63b6f65a67d44728c6d652636cb93e3 | 04-offlineSync-partial_failure | PNG ✅ | HTML ✅ | ✅ generated |
| empty | 11242ba793b3491380fe9fc5c836fc33 | 05-offlineSync-empty | PNG ✅ | HTML ✅ | ✅ generated |
| offline | c73186d3dc2240cea488324f1daaec69 | 06-offlineSync-offline | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/10780096558615730514/screens/73edb4992ae344d49117d7d63cbe787f) | — |
| content | [Open](https://stitch.google.com/projects/10780096558615730514/screens/47d285f3095b482b8f430ca05993803c) | — |
| syncing | [Open](https://stitch.google.com/projects/10780096558615730514/screens/d65b7747606b49659adb692be3953d11) | — |
| partial_failure | [Open](https://stitch.google.com/projects/10780096558615730514/screens/d63b6f65a67d44728c6d652636cb93e3) | — |
| empty | [Open](https://stitch.google.com/projects/10780096558615730514/screens/11242ba793b3491380fe9fc5c836fc33) | — |
| offline | [Open](https://stitch.google.com/projects/10780096558615730514/screens/c73186d3dc2240cea488324f1daaec69) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-field-officer-app --features offlineSync --force
```