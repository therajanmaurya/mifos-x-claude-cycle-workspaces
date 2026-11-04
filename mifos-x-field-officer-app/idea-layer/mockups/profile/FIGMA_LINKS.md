# FIGMA_LINKS.md — profile

<!-- schema: v3.2 | generated: 2026-11-04T10:33:53.549Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [10780096558615730514](https://stitch.google.com/projects/10780096558615730514) |
| Design System ID | 9551377288795375599 |
| Generated | 2026-11-04T10:33:53.338Z |
| Success | 5/5 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| loading | a2896a2db3714362b1ed55ec1496c6a3 | 01-profile-loading | PNG ✅ | HTML ✅ | ✅ generated |
| content | 817a72b171f74c60a9c2072246d8e394 | 02-profile-content | PNG ✅ | HTML ✅ | ✅ generated |
| error | e9a281d4ab21450c8af562b2794ddcfe | 03-profile-error | PNG ✅ | HTML ✅ | ✅ generated |
| offline | d7502b1c2d0f4f5f9c64d3f13c33038b | 04-profile-offline | PNG ✅ | HTML ✅ | ✅ generated |
| change_password | a1a088f2f16d41819d2c214130e77f2c | 05-profile-change_password | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| loading | [Open](https://stitch.google.com/projects/10780096558615730514/screens/a2896a2db3714362b1ed55ec1496c6a3) | — |
| content | [Open](https://stitch.google.com/projects/10780096558615730514/screens/817a72b171f74c60a9c2072246d8e394) | — |
| error | [Open](https://stitch.google.com/projects/10780096558615730514/screens/e9a281d4ab21450c8af562b2794ddcfe) | — |
| offline | [Open](https://stitch.google.com/projects/10780096558615730514/screens/d7502b1c2d0f4f5f9c64d3f13c33038b) | — |
| change_password | [Open](https://stitch.google.com/projects/10780096558615730514/screens/a1a088f2f16d41819d2c214130e77f2c) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-field-officer-app --features profile --force
```