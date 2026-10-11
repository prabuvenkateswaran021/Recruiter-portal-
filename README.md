# HR Recruiting Portal

A single-file, browser-based recruiting analytics dashboard. Upload your master candidate workbook (multi-tab Excel / Google Sheet export) and get a live Candidate Pipeline Report, interview tracking, requirement matching and monthly reports — with no server and no installation.

> **Live demo:** `https://<your-username>.github.io/<repo-name>/` (after you enable GitHub Pages — see [Deploy](#deploy-on-github-pages))

> 📘 **Client-friendly walkthrough:** see [CLIENT_GUIDE.md](CLIENT_GUIDE.md) for the full end-to-end process in plain language.

---

## Screenshots

| | |
|---|---|
| **Dashboard** ![Dashboard](docs/screenshots/02-dashboard.png) | **Charts & pivots** ![Charts](docs/screenshots/03-dashboard-charts.png) |
| **Upload – awaiting ingestion** ![Upload empty](docs/screenshots/04-upload-awaiting.png) | **Upload – validated** ![Upload loaded](docs/screenshots/05-upload-validated.png) |
| **Recruit Pro** ![Recruit Pro](docs/screenshots/07-recruit-pro.png) | **Interview Tracker** ![Interview Tracker](docs/screenshots/08-interview-tracker.png) |

All screenshots use anonymized sample data.

---

## Table of contents
1. [What it does](#what-it-does)
2. [How it works](#how-it-works)
3. [Quick start](#quick-start)
4. [Deploy on GitHub Pages](#deploy-on-github-pages)
5. [Upload process (Step 1: master workbook)](#upload-process)
6. [Required workbook format](#required-workbook-format)
7. [Modules](#modules)
8. [Login & roles](#login--roles)
9. [Data storage & privacy](#data-storage--privacy)
10. [Project structure](#project-structure)
11. [Tech stack](#tech-stack)
12. [Troubleshooting](#troubleshooting)
13. [Limitations & roadmap](#limitations--roadmap)

---

## What it does

| Area | Description |
|---|---|
| **Upload New Data** | Drag & drop a multi-tab workbook. The portal auto-maps the core sheets and previews them before publishing. |
| **Candidate Pipeline Report** | Submission-to-offer funnel, recruiter performance, client mix, daily trends, job roles, locations, engagement mode (FTE/C2H) and final status. |
| **Pivot tables** | Client × Final Status, Recruiter × Submission / Interview / Final Status, daily pipelines, plus a **Custom Pivot** builder. |
| **Filters** | Recruiter, Client, Mode, Submission status, Interview status, Final status, plus a date-range picker. |
| **Recruit Pro** | Upload client requirements and match them to candidates by Req ID. |
| **Interview Tracker** | Interview status counts by month/day and by recruiter/client. |
| **Monthly Reports** | Monthly dashboard with schedule creation. |
| **Export** | PDF export (jsPDF + html2canvas) and Excel export (SheetJS). |

## How it works

```
Master workbook (.xlsx / Google Sheet export)
        │  parsed in the browser (SheetJS)
        ▼
 Schema check ─► core sheets found?  Requirement tracker · INTERVIEW TRACKER STATUS · overall master sheet
        │
        ▼
 Preview (rows, recruiters, clients, date range, column check)
        │  "Publish to This Report"
        ▼
 Aggregation (in JS) ─► Dashboard, pivots, charts, filters
        │
        ▼
 Saved in the browser (localStorage) so data survives a refresh
```

Everything runs client-side. There is no backend, database or build step.

## Quick start

**Option A — open locally**
1. Download or clone the repo.
2. Double-click `index.html`.
3. Create the owner account on first launch, then sign in.

**Option B — local server (recommended if your browser blocks something)**
```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
python3 -m http.server 8000
# open http://localhost:8000
```

An internet connection is needed on first load because libraries (Chart.js, SheetJS, jsPDF, html2canvas) load from the jsDelivr CDN.

## Deploy on GitHub Pages

1. Create a new repository on GitHub (e.g. `hr-recruiting-portal`).
2. Add the files — either drag them into **Add file → Upload files**, or push from your computer:
   ```bash
   git init
   git add index.html README.md
   git commit -m "Initial commit: HR Recruiting Portal"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```
3. Open **Settings → Pages**.
4. Under **Build and deployment**, set **Source** to *Deploy from a branch*, choose **main** and **/ (root)**, then **Save**.
5. Wait 1–2 minutes. Your site will be live at `https://<your-username>.github.io/<repo-name>/`.

> ⚠️ **Do not commit real candidate data.** Candidate sheets contain personal data (names, phone numbers, emails, CTC). Keep the repo free of any real `.xlsx`/`.csv` files. If the repo is public, the portal code is public — the data is not, because it is uploaded only in each user's own browser.

## Upload process

Open **Upload New Data** in the left sidebar. The screen is titled **Candidate Data Management Portal**.

**STEP 1: Upload Your Master Candidate Sheet (Multi-Tab Workbook)**

1. **(Optional)** Click **Download Template Sheet** to get a blank workbook with the three core tabs and headers.
2. Fill in your data. Don't rename the core tabs.
3. **Drag & drop** your `.xlsx` onto the dropzone, or click **+ Upload Complete Google Sheet** to browse. (For a Google Sheet: *File → Download → Microsoft Excel (.xlsx)* first.)
4. **Schema check** — the portal looks for the three core sheets and marks each ✓ or ✕. If one is missing you get a warning and it falls back to the first usable sheet.
5. **Data Preview cards** update:
   - **Requirement TRACKER** — badges for *Recruiters, Mode of Hire, Client & Requirement, Candidate Tracker* turn green when the sheet is ingested.
   - **INTERVIEW TRACKER STATUS** — a Client / Value grid shows the first rows (skeleton rows are shown until a file is loaded).
6. Review the **Preview** (rows found, recruiters, clients, date range) and the **Column Check**.
7. Click **Publish to This Report**. The dashboard refreshes immediately.
8. Use **Choose a Different File** to reset and start over.

## Required workbook format

**Core sheets (tab names are matched case-insensitively):**

| Sheet | Purpose |
|---|---|
| `Requirement tracker` | Requirement data (recruiters, mode of hire, client & requirement) |
| `INTERVIEW TRACKER STATUS` | Client / Value interview status data |
| `overall master sheet` | The main candidate rows that drive the dashboard |

Extra tabs (e.g. `Sony`, `Indegene`, `INFOSYS`) are allowed and shown as chips but are not required.

**Columns expected in `overall master sheet`:**

```
Candidate Name, Candidate ID, Recruiter Name, Client, Mode of Req(FTE/C2H), Job Role, Req ID,
Skill Bucket, Date Of Submission, Profile Submission Status, Interview Status, Final Status,
Current Location, Mobile No, Email ID, Current Company, Payroll Company, Applied Location,
Total EXP, Rel EXP, Current CTC, EXP CTC, Notice Period /LWD
```

Missing columns are handled gracefully — the related charts or the candidate detail panel simply show less data. Header names must match exactly (extra spaces are trimmed). Dates should be real date cells; years outside 2015–2035 are ignored as invalid.

## Modules

- **Candidate Pipeline Report** — sections 00–18 including funnel, pivots, recruiter performance, trends and candidate drill-down.
- **Recruit Pro** — upload requirements, see detected column mapping, and view *Matched Candidates (by Req ID)*.
- **Interview Tracker** — upload interview data; month-wise and daily-wise counts overall, per recruiter and per client; custom pivot.
- **Monthly Reports Dashboard** — monthly view and *Create New Schedule*.
- **Sidebar tools** — reset filters, date-range picker, record count and generated date.

## Login & roles

- On first launch, create the **owner (admin)** account.
- Other people can **Sign up** and get the `user` role.
- Passwords are hashed (SHA-256 + per-user salt) before storage.

> ⚠️ **Important:** this is a static app, so login is a **convenience gate, not real security**. Anyone with browser dev tools can bypass it. Do not rely on it to protect sensitive data. For real access control, put the site behind authentication (e.g. Cloudflare Access, Netlify password protection, or a private hosting setup) or add a backend. The auth code is isolated in `AuthStore` so it can be swapped for a real provider.

## Data storage & privacy

- Uploaded data and accounts are stored in the **browser's localStorage** (via a small `window.storage` shim at the top of `index.html`), under keys prefixed `hrportal:`.
- Data stays on the user's device and is **never sent to a server** by this app.
- Data is **per browser and per device** — it is not shared between users. Clearing site data removes it.
- Each recruiter/manager must upload the workbook in their own browser, or you can adapt the app to a backend later.

## Project structure

```
.
├── index.html       # The whole app: HTML + CSS + JavaScript
├── README.md        # Technical overview and deployment
└── CLIENT_GUIDE.md  # End-to-end guide for clients/users
```

## Tech stack

- Vanilla HTML / CSS / JavaScript (single file)
- [Chart.js 4.4.1](https://www.chartjs.org/) — charts
- [SheetJS (xlsx 0.18.5)](https://sheetjs.com/) — Excel/CSV parsing and export
- [jsPDF 2.5.1](https://github.com/parallax/jsPDF) + [html2canvas 1.4.1](https://html2canvas.hertzen.com/) — PDF export
- Fonts: Space Grotesk, Inter, JetBrains Mono

## Troubleshooting

| Problem | Fix |
|---|---|
| Blank page / charts missing | Check your internet connection; the CDN scripts must load. |
| "Missing core sheet(s)" warning | Rename tabs to exactly `Requirement tracker`, `INTERVIEW TRACKER STATUS`, `overall master sheet`. |
| Chart shows little data | Check the **Column Check** for ✕ columns and fix header names. |
| Dates missing from trends | Make sure the date column holds real dates, not text like `N/A`. |
| Data gone after refresh | Browser is in private mode or blocks storage; use a normal window. |
| Google Sheet won't upload | Export it as `.xlsx` first (File → Download → Microsoft Excel). |
| GitHub Pages shows 404 | Ensure the file is named `index.html` in the repo root and Pages is set to `main` / root. |
| Large file is slow | Files with tens of thousands of rows parse in-browser; split by period if needed. |

## Limitations & roadmap

- No server-side authentication or shared database (data is per browser).
- Requires internet for CDN libraries (can be vendored locally for offline use).
- Ideas: backend/API with real auth, shared storage, direct Google Sheets API import, role-based views, vendored libraries for offline use.

## License

Add a license of your choice (e.g. MIT) as `LICENSE` in the repo root. This project handles personal data — use it in line with your organization's privacy policies.
