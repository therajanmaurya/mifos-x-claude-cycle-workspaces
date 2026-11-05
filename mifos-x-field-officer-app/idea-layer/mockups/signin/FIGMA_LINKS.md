# FIGMA_LINKS.md — signin

<!-- schema: v3.2 | generated: 2026-11-05T08:35:29.906Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [10780096558615730514](https://stitch.google.com/projects/10780096558615730514) |
| Design System ID | 9551377288795375599 |
| Generated | 2026-11-05T08:35:29.732Z |
| Success | 2/2 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| locked_out | 914c475e8e6a4d82ac4a1ccda7a836ff | 07-signin-locked_out | PNG ✅ | HTML ✅ | ✅ generated |
| success | 921e3b620e8849cfbf37ef991e14d49b | 08-signin-success | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| locked_out | [Open](https://stitch.google.com/projects/10780096558615730514/screens/914c475e8e6a4d82ac4a1ccda7a836ff) | — |
| success | [Open](https://stitch.google.com/projects/10780096558615730514/screens/921e3b620e8849cfbf37ef991e14d49b) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-field-officer-app --features signin --force
```