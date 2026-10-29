# Weekstack

A personal weekly schedule + daily checklist, built as an installable web app (PWA).
No build step, no framework: plain HTML/CSS/JS.

## Files
- `index.html` – the whole app (styles + script inside). The schedule lives in `myWeek()`.
- `manifest.webmanifest` – app name, colours, icons for "Add to Home Screen".
- `sw.js` – service worker so the app works offline. **Bump `VERSION` whenever any file changes.**
- `my-week.ics` – the same week as a repeating calendar with 10-minute alerts.
- `icons/` – app icons.

## How it works
- Schedule is saved in localStorage (`weekstack.v3`). Ticks are saved in `weekstack.checks` with today's date, and clear when the date changes.
- Items not ticked by their end time show as "Missed".
- Changing `myWeek()` only affects a fresh install or "Reset to my week".

## Hosting
Served by GitHub Pages from the `main` branch root. Pushing to `main` redeploys.
