# LCR Field Forms – setup guide (v2)

A free phone app for the daily pre-start, vehicle pre-start, incident/hazard reports and the fuel register. It replaces the GoCanvas forms.

- **Offline:** once installed, it works with no signal. Records stay on the phone until they're shared.
- **PDFs:** each record becomes a PDF in the same layout and file name style as GoCanvas, e.g. `24_11_2026_LCR_DAILY_PRESTART_00258.pdf`.
- **OneDrive:** tap **Share PDF**, pick **OneDrive** and choose the team folder. The OneDrive app must be installed and signed in.
- **No logins or user fees:** anyone with the link can install it.


## Version 2 – what's new
- **Laramide logo** on the app and on every PDF.
- **Daily pre-start** uses the GoCanvas lists: safety topics, work activities, tenements and prospects, people and supervisors. It adds:
  - a Journey Management Plan / sched book reminder when work or travel is off the tenements
  - a "not fit for work" warning.
- **Light vehicle pre-start** follows the GoCanvas trial version and your paper checklist (handbrake moved to Unit inspection):
  - four vehicle photos are required
  - any defect needs photos and comments
  - a warning shows when the next service is within 500 km
  - the tenement map can be opened from the work locations question.
- **Fuel register** follows the GoCanvas layout: fill location, which LV, odometer, fuel type, litres.
- **Team pack:** names, supervisors, phone numbers, vehicles and prospects are kept in a private file (`lcr-team-pack.json`). It is **not** on GitHub. Each phone imports it once: Settings → Import team pack.
- **SharePoint upload:** see `SETUP_SHAREPOINT.md`. Until IT has done that setup, use Share → OneDrive.

## Version 2.1
- **LV weekly inspection:** from the GoCanvas trial version, including recovery gear, engine bay and interior photos.
- **LV damage and maintenance report:**
  - Green / Amber / Red assessment, with tag-out prompts.
  - A maintenance status and a dated maintenance log you add to using *Edit*.
  - Can be started straight from a pre-start's defects: the vehicle, odometer, defects and photos are filled in for you.
- **Forklift pre-start:** uses hours and shift. The unit-inspection and housekeeping checks match GoCanvas. The electrical, engine bay and vehicle integrity checks are placeholders to confirm.

## Version 2.2
- **Journey management plan (LCR-SAF-FRM-008):**
  - Route templates fill in the stops, origin and destination. "Hells Gate – Mount Isa (dirt road)" and its reverse, Hells Gate – Doomadgee and back, and a custom route are included.
  - Mobile numbers fill in from the team pack for the traveller, passengers and sched monitor.
  - Covers alternative comms, how you'll contact the sched monitor, and sign-off.
- **Incident notification and investigation (LCR-SAF-FRM-003):** replaces the interim form. It has:
  - the GoCanvas pick-lists
  - witness statements in the witness's own words
  - a 5×5 risk matrix that sets the severity level (High / Extreme risk = Level 1; Medium = Level 2; Low = Level 3)
  - the person(s) involved, with fatigue and roster questions
  - injury details, the five groups of contributing factors, immediate and longer-term actions
  - declaration, supervisor sign-off, operator and SSE acceptance.

## Version 2.3 – Timesheet and expense claim
Both are on the home screen under **My month**. Set your name first: **Settings → Me**.
- **Timesheet:** one running sheet per month.
  - Today opens automatically. Tap **Worked**, **Travel** or **Day off / R&R**, pick the EPM/EL code and write the duties. **Same as previous day** copies yesterday's entry.
  - Work days are numbered automatically and totalled.
  - At month end, tap **Submit month** and sign. You get a PDF in the Lagoon Creek timesheet layout, named like `Oct_2026_Timesheet_MT.pdf`.
  - **Supervisor sign** adds their signature later.
- **Expense claim:** one running claim per month. Add each expense as it happens:
  - date, supplier, description, project, cost code
  - total incl. GST, with GST worked out as 1/11 automatically
  - receipts: take a photo, or attach a screenshot or PDF.
  
  **Submit claim** makes one PDF, named like `MT_expenses_October_26.pdf`: the claim page first, then every receipt, each labelled with its item. **Approver sign** adds the approval later.
- **Sending:** with SharePoint set up, PDFs upload to `Aus Geo Admin/06. Administration/03. Timesheets and Expense Claims/04. {YYYY}/{MM}. {Month}/{Name}`. Change the folder in Settings → Advanced, e.g. the `04.` year prefix each January. Otherwise use Share.
- **Reminders:** the home screen shows whether today's timesheet is filled in, and warns if last month wasn't submitted.

## Files
| File | Purpose |
|---|---|
| `index.html` | The whole app (the PDF library is built in) |
| `sw.js` | Service worker, the part that makes it work offline |
| `manifest.json`, `icon-*.png` | Home-screen name and icon |
| `app.html` | Editable source (`index.html` is built from it) |

## 1. Host it (free, about 10 minutes, once)
The app needs an `https://` web address so phones can install it. GitHub Pages is free:
1. Create a free GitHub account and a new **private** or public repository, e.g. `lcr-forms`. (Free Pages hosting on a private repo needs a paid plan. A public repo is fine because the repo holds no data, only the blank app.)
2. Upload `index.html`, `sw.js`, `manifest.json`, `icon-192.png` and `icon-512.png`.
3. Go to **Settings → Pages**, set Source to *Deploy from a branch* → `main` / root, then Save.
4. After a minute the app is live at `https://<username>.github.io/lcr-forms/`.

Netlify Drop (drag the folder onto app.netlify.com/drop) or Cloudflare Pages also work.

## 2. Install on each phone
- **iPhone/iPad:** open the link in **Safari** → Share → **Add to Home Screen**.
- **Android:** open it in **Chrome** → ⋮ menu → **Install app** (or *Add to Home screen*).

Open it once while you have signal so it caches for offline use.

## 3. First-time setup
1. **Settings:** enter crew names, vehicles, equipment and locations. Set the next pre-start number (e.g. **258** to continue from GoCanvas No. 00257). Give the device a name.
2. **Export settings** and send the file to other phones. They use **Import settings**.
3. Numbers count up separately on each phone. If two phones both do pre-starts, give each its own number block (e.g. one starts at 1000, the other at 2000).

## Daily use
- **Daily Pre-start:** fill it in, tap **Add all crew from list**, and each person ticks fit-for-work and signs on the screen. Tap **Save & make PDF**, then **Share PDF** → OneDrive.
  - Tip: open yesterday's record and tap **Start new from this** to copy over the location, supervisor and crew names (signatures are cleared).
- **Vehicle Pre-start:** answer every item, or use **Mark all unchecked items OK** after recording any defects. If you mark a vehicle safe despite a defect, the app asks for a note.
- **Incident / Hazard:** includes photos (from the camera or gallery) and GPS. Photos are embedded in the PDF.
- **Fuel register:** quick entries. At month end, go to **Fuel register → Share PDF register** or **Share CSV** (for Excel) → OneDrive.
- The home screen warns you about records not yet sent. **Settings → Back up all records** saves a full JSON backup.

## Limits to know about
- **Storage:** data lives in the phone's browser storage. Deleting the app, or clearing Safari/Chrome website data, deletes any records not yet shared. Share PDFs daily.
- **iPhone:** iOS can clear stored data for home-screen apps that haven't been opened for several weeks. This doesn't matter for daily use.
- **No automatic upload:** sending to OneDrive is the Share step (about two taps). Automatic upload into SharePoint/OneDrive is possible later. It needs your Microsoft 365 admin to register a free Azure app (Microsoft Graph); the app's code would then be extended to sign in and upload.
- **Editing forms:** fields are defined in the `FORMS` block near the top of the script in `app.html`. After editing, rebuild `index.html` (or ask Claude to). Change `VERSION` in `sw.js` so phones pick up the update next time they're online.
