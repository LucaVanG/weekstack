# Weekstack

A personal weekly schedule + daily checklist, built as an installable web app (PWA).
No build step, no framework: plain HTML/CSS/JS.

## Files
- `index.html` – the whole app (styles + script inside). The starting schedule is `DEFAULT_WEEK`.
- `manifest.webmanifest` – app name, colours, icons for "Add to Home Screen".
- `sw.js` – service worker so the app works offline. **Bump `VERSION` whenever any file changes.**
- `my-week.ics` – the same week as a repeating calendar with 10-minute alerts.
- `icons/` – app icons.

## How it works
- Three tabs: Day (checklist for one day), Week (hours by type + day strips), Types (rename, recolour, add, delete types).
- Data in localStorage `weekstack.v4`: `{types:[{id,name,color}], events:[{id,day(0=Mon),start,end(minutes),title,type,tasks:[{id,text,date?}]}]}`.
  A task with `date` (YYYY-MM-DD) is one-off; without it, it repeats every week on that block. Old one-off tasks are cleared automatically.
- Ticks live in `weekstack.checks4` as `{date, ids}` and clear when the date changes. Unticked blocks past their end time show as "Missed".
- Blocks can be split in two from the edit dialog. New blocks can be added to several days at once.
- `DEFAULT_WEEK` and `DEFAULT_TYPES` in index.html are only used on first open or "Reset to my week".

## Hosting
Served by GitHub Pages from the `main` branch root. Pushing to `main` redeploys.
