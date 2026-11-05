# FIGMA_LINKS.md — onboarding

<!-- schema: v3.2 | generated: 2026-11-05T06:26:54.850Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [10780096558615730514](https://stitch.google.com/projects/10780096558615730514) |
| Design System ID | 9551377288795375599 |
| Generated | 2026-11-05T06:26:54.604Z |
| Success | 3/3 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| intro_clients | 99fd140a61c74a36833f11c39627074f | 01-onboarding-intro_clients | PNG ✅ | HTML ✅ | ✅ generated |
| intro_collections | e7427ee8ab0a4fa4b1f9efdb9a359508 | 02-onboarding-intro_collections | PNG ✅ | HTML ✅ | ✅ generated |
| intro_offline | 283d76c0b569458e9f4c5aac49423b29 | 03-onboarding-intro_offline | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| intro_clients | [Open](https://stitch.google.com/projects/10780096558615730514/screens/99fd140a61c74a36833f11c39627074f) | — |
| intro_collections | [Open](https://stitch.google.com/projects/10780096558615730514/screens/e7427ee8ab0a4fa4b1f9efdb9a359508) | — |
| intro_offline | [Open](https://stitch.google.com/projects/10780096558615730514/screens/283d76c0b569458e9f4c5aac49423b29) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-field-officer-app --features onboarding --force
```