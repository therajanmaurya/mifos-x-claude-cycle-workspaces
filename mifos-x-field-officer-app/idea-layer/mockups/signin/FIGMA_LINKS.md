# FIGMA_LINKS.md — signin

<!-- schema: v3.2 | generated: 2026-11-04T10:44:50.758Z -->

## Stitch Project

| Field | Value |
|-------|-------|
| Project URL | [10780096558615730514](https://stitch.google.com/projects/10780096558615730514) |
| Design System ID | 9551377288795375599 |
| Generated | 2026-11-04T10:44:50.473Z |
| Success | 8/8 states |

## Screen Status

| State | Screen ID | Folder | PNG | HTML | Status |
|-------|-----------|--------|-----|------|--------|
| empty | 24441b57af364de4b373cf85506e638f | 01-signin-empty | PNG ✅ | HTML ✅ | ✅ generated |
| biometric_ready | cd50d5f3869d43bcbd006852f663db64 | 02-signin-biometric_ready | PNG ✅ | HTML ✅ | ✅ generated |
| submitting | 37236d56b0c542969f408e0a0fec4568 | 03-signin-submitting | PNG ✅ | HTML ✅ | ✅ generated |
| validation_error | 76e8f687f7ba47f9a97d3c06dfb60a71 | 04-signin-validation_error | PNG ✅ | HTML ✅ | ✅ generated |
| transport_error | ca6abe9d5cf241e383178601744df9eb | 05-signin-transport_error | PNG ✅ | HTML ✅ | ✅ generated |
| offline | 4b130f5116884d30b249646c81f59878 | 06-signin-offline | PNG ✅ | HTML ✅ | ✅ generated |
| locked_out | 16c0c7aae52841b1b2cb7fd70b7939d9 | 07-signin-locked_out | PNG ✅ | HTML ✅ | ✅ generated |
| success | 449c9dd966664628be31cf990b217fd0 | 08-signin-success | PNG ✅ | HTML ✅ | ✅ generated |

## Open in Figma / Stitch

| State | Stitch Screen | Figma Export |
|-------|--------------|--------------|
| empty | [Open](https://stitch.google.com/projects/10780096558615730514/screens/24441b57af364de4b373cf85506e638f) | — |
| biometric_ready | [Open](https://stitch.google.com/projects/10780096558615730514/screens/cd50d5f3869d43bcbd006852f663db64) | — |
| submitting | [Open](https://stitch.google.com/projects/10780096558615730514/screens/37236d56b0c542969f408e0a0fec4568) | — |
| validation_error | [Open](https://stitch.google.com/projects/10780096558615730514/screens/76e8f687f7ba47f9a97d3c06dfb60a71) | — |
| transport_error | [Open](https://stitch.google.com/projects/10780096558615730514/screens/ca6abe9d5cf241e383178601744df9eb) | — |
| offline | [Open](https://stitch.google.com/projects/10780096558615730514/screens/4b130f5116884d30b249646c81f59878) | — |
| locked_out | [Open](https://stitch.google.com/projects/10780096558615730514/screens/16c0c7aae52841b1b2cb7fd70b7939d9) | — |
| success | [Open](https://stitch.google.com/projects/10780096558615730514/screens/449c9dd966664628be31cf990b217fd0) | — |

> **Figma Export**: direct download URL captured from Stitch SDK `screen.data.figmaExport.downloadUrl`. May be `—` if Stitch did not generate a Figma export for this screen.
>
> **Stitch Screen**: opens the screen in Stitch web UI — use the Figma export button there for native Figma transfer.

## Re-run

```bash
STITCH_API_KEY=<key> deno run --allow-env --allow-net --allow-read --allow-write \
  .claude-runtime/scripts/stitch-generate.ts \
  --workspace mifos-x/mifos-x-field-officer-app --features signin --force
```