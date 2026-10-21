# Amman Christmas Market — Entertainment Scheduler

Single file: `index.html`. No installation, server, account or internet connection needed.

## 1. Opening it
1. Save `index.html` anywhere (e.g. a shared drive folder or your desktop).
2. Double-click it to open in Chrome, Edge, Firefox or Safari (desktop or tablet).
3. It opens with fictional demo data, each record marked **DEMO — NOT A REAL BOOKING**. Remove it any time from the Dashboard banner or *Settings → Data* (your own events are kept).

## 2. Using it
| View | What it is for |
|---|---|
| **Dashboard** | Counts by type/status, days needing scheduling, unscheduled time, open warnings, special dates, dense performers. Click a day for its summary. |
| **Month** | Sun–Sat calendar of Nov/Dec 2026. Market days have a gold edge; each shows hours, programming status, warnings and up to 3 events (“+N more”). Click a day → its timeline; click an event → edit. |
| **Day timeline** (main tool) | Time runs horizontally. Each stage is a row, and each roaming group has its own row (roaming acts move around the whole market, so they have no location). Click an empty slot to add an event there. Drag to move (stage acts can also move to another stage), drag edges to resize, or focus a block and use arrow keys (Shift+arrow = end time). Compact/detailed, zoom, collapsible rows. |
| **Week** | Seven days side by side, each with its own hours. Drag up/down to change time, sideways to change day. |
| **Schedule** | Searchable, sortable master table with column picker; date/time/title/status edit inline (changing the date moves the event). Duplicate, delete. **Run of show** mode lists one day chronologically with call times, contacts, technical needs and notes. |
| **Warnings** | Every warning with date, time, events, reason, links, filters, and *Acknowledge* (with note). |
| **Settings** | Five tabs: *Dates & hours* (market dates, weekly hours, date overrides/special events), *Stages*, *Performers & categories*, *Warning rules* (incl. coverage targets), *Backup & data*. Rarely used options sit under “Advanced” toggles. |

The toolbar date selector, search and **New event** work across all views. Category/performer/location/status/type filters open from the **Filters** button (a number shows how many are active). The legend shows the basics; **Colours & help** reveals category colours and how-to tips. **↶** (Ctrl+Z) undoes the last change.

**Event editor:** opens with just the essentials (title, date, times, type, stage (stage acts only), performer, category, status); contact, notes, setup/changeover times, priority and budget are under **More details**. Only title, date, start and end are required. It shows warnings live before saving and supports setup/sound-check/changeover/break times, contacts, notes, fee and special event. *Cancel appearance* keeps the record (struck through, excluded from checks). *Repeat on other dates / Create additional appearances* picks weekdays or specific dates, previews every date with clashes, and can skip clashing dates — existing events are never overwritten.

## 3. Saving, backups and moving to another computer
- Every change saves automatically to **this browser only** (IndexedDB; localStorage fallback). The top bar shows *Saved* / *Unsaved changes*. It does **not** sync between computers or people, and clearing browser data deletes it.
- **Export backup (JSON):** *Export / Print* button or *Settings → Data*. Do this regularly and before handing over.
- **Import backup:** validated first (format, version, dates, times, IDs); a summary and an overwrite warning appear; an automatic **restore point** of the current data is taken before replacing. Invalid files are rejected and nothing changes.
- **Restore points:** last 6 snapshots (before import, reset, restore, demo removal, or manual) — restore or download them in *Settings → Data*.
- **Reset everything** requires typing RESET.
- To move to another device: export backup → copy the file → open `index.html` there → import.

**Exports:** CSV (all, date range, one day, or the current filtered table; UTF-8 with BOM so Arabic opens correctly in Excel). PDF: choose a report (run of show, daily timeline, monthly calendar, master schedule for a date range) and click *Print / Save as PDF*, then pick **“Save as PDF”** as the printer. Navigation and controls are omitted from print.

## Shared online version (claude.ai link)
The same app is also published as a private claude.ai page. In shared mode the schedule is stored online instead of in one browser, so everyone with access sees the same data and each other's changes live.
- **Share it** from the page's Share menu. People need a claude.ai account and must be signed in. **Contributor** or **Editor** = can view and edit; **Viewer** or **Commenter** = view and export only (the page shows a “View only” banner).
- Each person picks their own language; it isn't shared.
- Two people editing *different* events never clash. If two people save the *same* event at the same moment, the later save wins.
- Printing isn't possible inside the shared page, so the print buttons save a printable .html file instead: open it and choose “Save as PDF”. CSV and backup files are saved through a confirmation prompt.
- To move a schedule you built in the offline file into the shared page: *Export backup* in the file, then *Import backup* on the shared page (this replaces the shared schedule for everyone).

## 4. How hours, overlaps and special Tuesdays work
- **Hours** come from *Default weekly hours* (Sun–Thu 4–11 PM, Fri–Sat 11 AM–11 PM) unless a **date override** exists. Dates outside the market range are treated as closed. All times are Amman local time (Asia/Amman); nothing depends on the computer’s time zone.
- **Date overrides** apply to one date only: *Default hours*, *Custom hours* (e.g. 6–11 PM) or *Closed*, plus an optional **special event** flag with name, description and its own time window.
- **Special Tuesdays** are never automatic. *Add special Tuesday* creates a 6–11 PM override for that single date. To keep the market opening at 4 PM while the special programme runs 6–11 PM, set hours to *Default* and only fill in the special event time (demo: Dec 1 = overridden hours, Dec 8 = normal hours + special window).
- **Overlaps are warnings, never blocks.** Stage and roaming acts can run at the same time freely. Flagged: same stage double-booked, same performer in two places, changeover gap shorter than the rule/setup/sound-check, rest/recovery gaps shorter than an act’s “break after” time or the global minimum, daily-load limits (off by default), events before opening/after closing/on closed days, and confirmed/tentative records missing performer, category, location or contact.
- Recovery between roaming sets is handled by the break rule: set “Required break after” on an act (or a global minimum in *Warning rules*) and the next appearance of the same group is flagged if it starts too soon.
- **Acknowledged** warnings become “intentional”, keep their note, and stay listed.
- **Coverage targets** are off by default, so days show “Scheduled” or “Needs scheduling” — never “Complete”. Turn them on (stage % of open hours, minimum roaming appearances) to get Complete / Partial.
- **Arabic:** the whole interface switches to RTL. On the timeline, time runs right (earlier) → left (later), matching reading direction; positions are computed from real times. Names, notes and titles you type are never translated. Digits stay 0–9.

## 5. Testing performed
Automated in headless Chromium against the built `index.html` (102/102 checks passing, including the simplified layout, the zone-free roaming rows, and importing older backups that still contain zones), plus visual review of screenshots in English and Arabic and of the generated PDFs. Verified:
- Dates: 19 days, Nov 25 = Wednesday, Dec 13 = Sunday, every weekday cross-checked; default hours; a special override on one date leaves others and weekly Tuesday unchanged; closed and custom hours for any date; timeline axis starts at 4 PM / 11 AM / 6 PM as appropriate.
- Editing: create, edit, duplicate, delete-with-confirmation; invalid/zero-length times rejected; mouse drag (+60 min), resize (duration 45→75), keyboard nudge, roaming acts move in time but stay in their group row, stage acts blocked from roaming rows, week cross-day drag, undo; click-to-create prefill; recurring events with preview, clash skipped, existing events untouched; edits visible in month, week, day and table.
- Conflicts: different-resource overlap not flagged; same-stage overlap, performer double booking, too little recovery between roaming sets, outside/after hours and incomplete records flagged; recalculation after a move; acknowledgement with note stays visible; panel filters.
- Persistence: reload keeps events + settings + acknowledgements; backup contents; invalid and non-JSON backups rejected without change; import warning, full restore, automatic restore point; demo removal keeps user events; reset needs typed confirmation; corrupted stored data handled with a message and the raw data preserved.
- Exports: CSV BOM, row counts, escaping of commas/quotes/line breaks, Arabic preserved, day/range/filtered scopes; all four print reports rendered to PDF (portrait run of show; landscape others) with the UI hidden.
- Arabic/accessibility: lang/dir switch, Arabic labels and editor, chronological RTL axis and block positions; every visible control has an accessible name in every view; no network requests; no JavaScript errors.

Not verified automatically: Firefox/Safari (tested in Chromium only), real touch-screen dragging, and the browser’s own print dialog (the print layout was verified by generating PDFs directly).

## 6. Limitations
- Storage is per browser profile; no multi-user sync or real-time collaboration. Use backup files to share.
- PDF uses the browser’s print dialog (“Save as PDF”), not a one-click file download — this keeps the app fully offline with no external library.
- Native date/time pickers follow the computer’s locale (e.g. mm/dd/yyyy, AM/PM) rather than the app language.
- Overnight events (past midnight) are supported only when enabled in Settings, and appear on their start date.
- Drag snapping minimum is 1 minute; drag cannot extend an event past 23:55 unless overnight events are enabled.
- In Arabic, long Latin titles inside narrow timeline blocks truncate from the start; full text is in the tooltip and editor.
- Toast notifications appear at the bottom of the screen and can briefly cover the lowest timeline row.
- All interface text is translated; only user-entered data and the “DEMO” marker inside small blocks remain in their original language.
