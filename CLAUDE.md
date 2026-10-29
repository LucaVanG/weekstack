# Weekstack

A personal weekly schedule + daily checklist, built as an installable web app (PWA).
No build step, no framework: plain HTML/CSS/JS.

## Files
- `index.html` – the whole app (styles + script inside). The starting schedule is `DEFAULT_WEEK` (both weeks) plus `WORK_FRIDAY` (Week 1's Friday afternoon).
- `manifest.webmanifest` – app name, colours, icons for "Add to Home Screen".
- `sw.js` – service worker so the app works offline. **Bump `VERSION` whenever any file changes.**
- `my-week.ics` – the same fortnight as a repeating calendar with 10-minute alerts. Blocks that differ between the weeks repeat with `INTERVAL=2`.
- `icons/` – app icons.

## How it works
- The plan is a two-week cycle. Week 1 (the week with a Friday work shift) starts Mon 26 Oct 2026 (`CYCLE_START`), then every 14 days.
- Three tabs: Day (checklist for one day, picked from this week + next week), Week (fortnight hours by type + day strips), Types (rename, recolour, add, delete types).
- Data in localStorage `weekstack.v5`: `{types:[{id,name,color}], events:[{id,day(0–13: 0–6 Week 1, 7–13 Week 2, 0=Mon),start,end(minutes),title,type,tasks:[{id,text,date?}]}]}`.
  A task with `date` (YYYY-MM-DD) is one-off; without it, it repeats every fortnight on that block. Old one-off tasks are cleared automatically.
  Old `weekstack.v4` data (one week) is copied into both weeks on first open, with the work shift added to Week 1's Friday.
- Ticks live in `weekstack.checks5` as `{cycle, ids}` and clear when a new fortnight starts. Today and earlier days this week can be ticked; unticked blocks past their end time show as "Missed".
- Blocks can be split in two from the edit dialog. New blocks can be added to several days at once.
- `DEFAULT_WEEK`, `WORK_FRIDAY` and `DEFAULT_TYPES` in index.html are only used on first open or "Reset to my fortnight".

## Hosting
Served by GitHub Pages from the `main` branch root. Pushing to `main` redeploys.
