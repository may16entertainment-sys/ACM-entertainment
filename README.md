# Amman Christmas Market — Entertainment Scheduler

Two ways to use it:
- **Shared online (GitHub Pages + Firebase):** everyone with the schedule's link sees the same schedule live; only people you add in the **Editors** tab can sign in (Google, or email + password) and change it. The site's main address is a sign-in page that takes editors straight to the schedule. The owner, **may16entertainment@gmail.com**, is admin of every schedule. Setup is in section 0 below.
- **Offline:** double-click `index.html` on any computer. Everything is saved in that browser only.

Files: `index.html` (the app), `firebase-config.js` (which Firebase project to use), `firestore.rules` (who may read and write), `README.md` (this guide).

## 0. Setting up the shared online version (one time, about 20 minutes)

You need a free Google account (for Firebase) and a free GitHub account. Never put passwords in any of these files: the GitHub repository is public.

### A. Create the Firebase database
1. Go to **console.firebase.google.com** and sign in with your Google account.
2. Click **Create a project** (or **Add project**). Name it, for example `amman-market-schedule`. You can turn Google Analytics off. Click through to finish.
3. In the left menu open **Build → Authentication**, click **Get started**, and open the **Sign-in method** tab. Turn on two providers:
   - **Email/Password**: switch the first toggle **on** (leave *Email link* off) and **Save**. Editors sign in with this.
   - **Anonymous**: switch it **on** and **Save**. Viewers use this behind the scenes; they never create an account.
   - **Google**: click **Add new provider → Google**, switch it **on**, pick your email as the *support email*, and **Save**. The owner signs in with this, and so can any editor whose Google email you add.
4. In the left menu open **Build → Firestore Database** and click **Create database**. Pick a location close to Jordan (for example a Europe location) and choose **production mode**. Click **Create**.
5. In Firestore, open the **Rules** tab. Delete everything in the box, paste the entire contents of `firestore.rules`, and click **Publish**.
6. Click the gear icon next to *Project Overview* → **Project settings**. Under **Your apps**, click the web icon **`</>`**. Give it a nickname (e.g. `scheduler`), leave *Firebase Hosting* unticked, and click **Register app**.
7. Firebase shows a block of code containing `apiKey`, `authDomain`, `projectId` and so on. Open `firebase-config.js` and replace each `PASTE…` value with the matching value from Firebase (keep the quotes). These values are not secret.

### B. Publish on GitHub Pages
1. On **github.com**, click **+** → **New repository**. Name it (e.g. `amman-market-schedule`), choose **Public**, click **Create repository**.
2. Click **uploading an existing file** and drag in `index.html`, `firebase-config.js`, `firestore.rules` and `README.md`. Click **Commit changes**.
3. Open **Settings → Pages**. Under *Build and deployment* choose **Deploy from a branch**, branch **main**, folder **/ (root)**, and **Save**.
4. After a minute or two, refresh that page: it shows your site address, like `https://yourname.github.io/amman-market-schedule/`.
5. Back in Firebase: **Authentication → Settings → Authorized domains → Add domain**, and add `yourname.github.io` (your GitHub username + `.github.io`). Google sign-in does not work until this is done.

### C. Create the shared schedule
1. Open your site address. It shows the sign-in page.
2. Click **Sign in with Google** and choose **may16entertainment@gmail.com**. Only this account can set up schedules; it is written into `index.html` (`FB_OWNER`) and `firestore.rules`.
3. Click **Set up a new shared schedule**, then **Sign in with Google and create**.
4. The schedule opens with its own private link (`…/?s=…`). From now on, signing in at the main address opens it directly. Viewers still need this link, so bookmark it.
5. To bring in the schedule you already built: in your offline `index.html`, *Export backup (JSON)*; then on the shared page click **Import backup** (or use the button on the empty-schedule banner).

### D. Share it
- **To let someone view:** send them the link (top bar → **👤 Account** → *Copy*).
- **To let someone edit:** open the **Editors** tab (admins only), type their email, choose **Editor** (or **Admin** if they should also manage people) and click **Create**. A password is made for them. Click **Copy invitation** — it copies the link, their email and password — and paste it into a message to them. The password is shown only once, so copy it before leaving the page.
- **How editors sign in:** they go to the site's main address and sign in (Google, or the email and password from the invitation), and the schedule opens. Or they open the schedule link and click **🔒 Sign in to edit**. They stay signed in on that browser until they choose *Sign out* (under 👤 Account). Someone with a Gmail address can use **Sign in with Google** instead of the generated password.
- **Forgotten password:** they click *Forgot password?* on the sign-in screen, or an admin clicks **Send password reset** next to their name. Firebase emails them a link to choose a new one (check spam).
- **To remove someone's editing access:** **Editors** tab → **Remove**. It takes effect immediately; they can still view if they have the link.
- **To remove someone's viewing access:** the link cannot be changed. Export a backup, set up a new shared schedule, import the backup, and share the new link.

### E. Changing the logo
Make a square image (PNG, about 256 × 256 pixels, transparent background looks best), name it exactly **`logo.png`**, and upload it to the repository next to `index.html`. It replaces the Christmas-tree logo in the top bar and on the sign-in page within a couple of minutes. Delete `logo.png` to go back to the tree.

### F. Updating the app later
Upload a new `index.html` to the repository the same way (it replaces the old one). The schedule data lives in Firebase and is not affected.

### G. Setting up another schedule (owner)
Go to the main address with `?setup` on the end (for example `https://yourname.github.io/amman-market-schedule/?setup`), signed in as the owner, and choose *Set up a new shared schedule*. The sign-in page opens the newest schedule from then on; older ones still work from their own links.

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
- *Offline version:* every change saves automatically to **this browser only** (IndexedDB; localStorage fallback). The top bar shows *Saved* / *Unsaved changes*. It does **not** sync between computers or people, and clearing browser data deletes it.
- **Export backup (JSON):** *Export / Print* button or *Settings → Data*. Do this regularly and before handing over.
- **Import backup:** validated first (format, version, dates, times, IDs); a summary and an overwrite warning appear; an automatic **restore point** of the current data is taken before replacing. Invalid files are rejected and nothing changes.
- **Restore points:** last 6 snapshots (before import, reset, restore, demo removal, or manual) — restore or download them in *Settings → Data*.
- **Reset everything** requires typing RESET.
- To move to another device: export backup → copy the file → open `index.html` there → import.

**Exports:** CSV (all, date range, one day, or the current filtered table; UTF-8 with BOM so Arabic opens correctly in Excel). PDF: choose a report (run of show, daily timeline, monthly calendar, master schedule for a date range) and click *Print / Save as PDF*, then pick **“Save as PDF”** as the printer. Navigation and controls are omitted from print.

## Shared online version: how it behaves
- Everyone with the link sees the same data, and each other's changes appear within a second or two.
- Viewers see a “View only” banner. They can browse, filter, print and export, but not change anything.
- Each person picks their own language; it isn't shared.
- Two people editing *different* events never clash. If two people save the *same* event at the same moment, the later save wins.
- If an admin removes you while you are editing, your next change is refused and the page switches to view-only, showing the shared copy.
- **Import backup** on the shared page replaces the shared schedule for everyone.
- Restore points and undo work per browser, as in the offline version. Export a backup from time to time.

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

Shared online version: tested in headless Chromium against a stand-in for Firebase that applies the same access rules: the Editors tab and invitations (34/34 checks), plus the sign-in main page, Google sign-in, the owner account, owner-only set-up, editors taken straight to the schedule, strangers and a fake unverified "owner" account refused, Arabic sign-in page, and logo.png (34/35; the one failure was the test stand-in losing a connection when the test navigated away, not the app). Not yet run against a live Firebase project.

Not verified automatically: Firefox/Safari (tested in Chromium only), real touch-screen dragging, and the browser’s own print dialog (the print layout was verified by generating PDFs directly).

## 6. Limitations
- Offline version: storage is per browser profile, with no sync. Use the shared online version (section 0) to work together.
- Shared online version: needs an internet connection. Anyone with the schedule link can view, so share it only with people who should see it. The site's main address is public but shows only the sign-in page; only the owner can set up schedules. Firebase's free plan is far more than one market schedule needs.
- The app records who may edit, but not who made each individual change.
- Admins cannot remove themselves; another admin can remove them. The owner (may16entertainment@gmail.com) can never be removed and is admin of every schedule. To hand ownership to another Google account, change the email in both `index.html` (`FB_OWNER`) and `firestore.rules`, then upload/publish both.
- Accounts belong to your Firebase project, not to one schedule. Removing someone from the Editors list ends their editing but keeps their account; adding them again later re-uses it (they keep their old password). To delete accounts completely, use Firebase → Authentication → Users.
- PDF uses the browser’s print dialog (“Save as PDF”), not a one-click file download — this keeps the app fully offline with no external library.
- Native date/time pickers follow the computer’s locale (e.g. mm/dd/yyyy, AM/PM) rather than the app language.
- Overnight events (past midnight) are supported only when enabled in Settings, and appear on their start date.
- Drag snapping minimum is 1 minute; drag cannot extend an event past 23:55 unless overnight events are enabled.
- In Arabic, long Latin titles inside narrow timeline blocks truncate from the start; full text is in the tooltip and editor.
- Toast notifications appear at the bottom of the screen and can briefly cover the lowest timeline row.
- All interface text is translated; only user-entered data and the “DEMO” marker inside small blocks remain in their original language.
