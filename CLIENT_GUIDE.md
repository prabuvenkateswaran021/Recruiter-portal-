# HR Recruiting Portal — Client Guide (End to End)

This guide explains, in plain language, what the portal does, what you need to prepare, how to use it step by step, and how to read the results. No technical knowledge is required.

---

## 1. What is this portal?

The HR Recruiting Portal turns your recruitment tracking spreadsheet into a live dashboard. Instead of manually counting submissions, interviews and offers in Excel, you upload one workbook and the portal shows:

- How many candidates were submitted, interviewed, selected or rejected
- How each recruiter and each client is performing
- Daily and monthly trends
- Which candidates match which open requirement

**Key points to know up front**
- It runs in your web browser. Nothing is installed.
- Your file is read inside your own browser. It is **not uploaded to any server** by this portal.
- Data is saved in the browser you used, on that device. Another person or another device will need to upload the file again.

---

## 2. The big picture (end to end)

```
1. Prepare workbook  →  2. Open portal & sign in  →  3. Upload workbook
        →  4. Check validation & preview  →  5. Publish
        →  6. Explore dashboard (filters, pivots)  →  7. Use Recruit Pro / Interview Tracker / Monthly Reports
        →  8. Export reports  →  9. Refresh with new data (repeat step 3)
```

---

## 3. Step 1 — Prepare your master workbook

You need **one Excel file (.xlsx)** with several tabs (sheets). If you keep your tracker in Google Sheets, download it first: **File → Download → Microsoft Excel (.xlsx)**.

### 3.1 Three tabs are mandatory

| Tab name (must match) | What it contains |
|---|---|
| **Requirement tracker** | Your open requirements: recruiter, mode of hire, client, requirement details |
| **INTERVIEW TRACKER STATUS** | Interview status summary, in a Client / Value layout |
| **overall master sheet** | One row per candidate submission. This is the main data source for the dashboard |

Tab names are not case-sensitive, but spelling must match. Other tabs (for example one per client such as *Sony*, *Indegene*, *INFOSYS*) are allowed and will appear as tabs in the preview, but are not required.

### 3.2 Columns for the "overall master sheet"

| Group | Columns |
|---|---|
| Candidate | Candidate Name, Candidate ID, Mobile No, Email ID |
| Recruiting | Recruiter Name, Client, Mode of Req(FTE/C2H), Job Role, Req ID, Skill Bucket |
| Pipeline | Date Of Submission, Profile Submission Status, Interview Status, Final Status |
| Profile | Current Location, Applied Location, Current Company, Payroll Company, Total EXP, Rel EXP |
| Compensation | Current CTC, EXP CTC, Notice Period /LWD |

### 3.3 Data quality tips (these decide how accurate your dashboard is)

1. **Use the exact column names above.** A renamed column will show as ✕ in the Column Check and the related chart will be empty.
2. **Dates must be real dates**, not text such as "N/A" or "pending". Dates outside 2015–2035 are treated as errors and ignored.
3. **Use consistent spellings** for clients, recruiters and statuses. "Infosys", "INFOSYS" and "Infosys Ltd" may be counted separately (the portal already merges common variants such as Infosys and Uniquehire Internal).
4. **Keep one header row** at the top, with no merged cells above it.
5. **Do not leave blank rows** in the middle of data.
6. Locations such as Bangalore/Bengaluru and Gurgaon/Gurugram are normalized automatically.

> Tip: click **Download Template Sheet** in the portal to get a blank workbook with the correct tabs and headers, then paste your data in.

---

## 4. Step 2 — Open the portal and sign in

1. Open the portal link supplied to you.
2. **First time only:** the owner (administrator) creates the owner account — name, email, password.
3. Other team members click **Sign up** to create their own accounts. They get the standard *user* role.
4. Sign in with email and password. Tick **Keep me signed in** if you want to stay logged in.

![First-time owner setup](docs/screenshots/01-owner-setup.png)

**Please note:** the sign-in is a basic gate for convenience. It is not enterprise-grade security. If the data is highly sensitive, ask your administrator to place the portal behind company access control.

---

## 5. Step 3 — Upload the workbook

Click **↑ Upload New Data** in the left sidebar. The screen is titled **Candidate Data Management Portal**.

### What you will see

| Screen area | What it is for |
|---|---|
| **STEP 1: Upload Your Master Candidate Sheet (Multi-Tab Workbook)** | Header of the upload step |
| Sheet preview with tab chips | Shows the tabs of a typical workbook; after upload it shows *your* tabs |
| Dropzone | Drag and drop your .xlsx here, or click **+ Upload Complete Google Sheet** to browse |
| **Schema check** box | Lists the three required sheets and ticks them after upload |
| **Download Template Sheet** | Gets a blank correct-format workbook |
| **Requirement TRACKER** card | Shows ingestion status of the requirement data |
| **INTERVIEW TRACKER STATUS** card | Shows the first rows of interview data |

### How to upload


**Before a file is loaded (empty state):**

![Upload screen awaiting ingestion](docs/screenshots/04-upload-awaiting.png)
1. Drag your .xlsx file into the dropzone, or click the upload button and pick the file.
2. The file name and size appear, and the portal reads it.
3. Your actual tab names replace the sample chips.

**After a file is loaded (schema check ✓, cards populated):**

![Upload screen validated](docs/screenshots/05-upload-validated.png)

---

## 6. Step 4 — Validate and preview before publishing

After the file is read, check four things:

1. **Schema check** — each of the three core sheets should show ✓. A ✕ means that tab is missing or misnamed. The portal will warn you and use the first usable sheet instead, but results may be incomplete.
2. **Requirement TRACKER card** — changes from "Awaiting Ingestion" to "Ingested" with a row count. The four badges (Recruiters, Mode of Hire, Client & Requirement, Candidate Tracker) turn green.
3. **INTERVIEW TRACKER STATUS card** — the grey placeholder rows are replaced by real Client / Value rows from your file.
4. **Preview + Column Check** — shows rows found, number of recruiters, number of clients and the date range, plus a ✓/✕ list of expected columns.

### What to do if something looks wrong

| You see | Meaning | Action |
|---|---|---|
| ✕ on a core sheet | Tab name is wrong or missing | Rename the tab, save, upload again |
| ✕ on a column | Column header is missing or spelled differently | Fix header, upload again |
| Rows found is 0 | The sheet is empty or headers are not in row 1 | Check the master sheet layout |
| Date range looks odd | Some date cells are text or typos | Correct dates in the sheet |

Click **Choose a Different File** to start over at any time.

**Preview, column check and Publish button:**

![Preview and publish](docs/screenshots/06-upload-preview-publish.png)

---

## 7. Step 5 — Publish

When the preview looks right, click **Publish to This Report**. The dashboard updates immediately and the data is saved in your browser, so it is still there next time you open the portal on the same device.

---

## 8. Step 6 — Read the Candidate Pipeline Report

The main report is built from the **overall master sheet**.

### 8.1 Filters (top of the page)

![Candidate Pipeline Report](docs/screenshots/02-dashboard.png)
Recruiter, Client, Mode (FTE / C2H), Submission status, Interview status, Final status, and a **Date Range** picker in the sidebar. Every chart and table responds to the filters. Use **Reset Filters** to clear everything.

### 8.2 Key sections

| Section | What it tells you |
|---|---|
| Submission-to-Offer Funnel | How many candidates move from submitted → reviewed → interviewed → selected |
| Submissions by Recruiter | Who submitted how many profiles |
| Client Mix | Share of submissions per client |
| Daily Submission Trend | Activity over time |
| Top Job Roles | Roles with the most submissions |
| Candidate Locations | Where candidates are located |
| Profile Submission Status | Accepted, pending, rejected breakdown |
| Engagement Mode | FTE vs C2H split |
| Final Status by Recruiter | Selected / rejected / on-hold per recruiter |
| Recruiter Performance | Overall comparison across recruiters |

### 8.3 Pivot tables

![Charts and pivots](docs/screenshots/03-dashboard-charts.png)
Ready-made pivots include Client × Final Status, Recruiter × Submission Status, Recruiter × Interview Status, Recruiter × Final Status, Recruiter × Client × Final Status, daily pipelines (date × client × recruiter) and total submissions by recruiter. A **Custom Pivot** lets you choose your own row and column fields.

### 8.4 Candidate drill-down
Click a chart bar, number or pivot cell to see the matching candidates. The candidate detail panel shows contact and profile details, limited to the columns present in your file.

---

## 9. Step 7 — Other modules

### Recruit Pro (requirement matching)

![Recruit Pro](docs/screenshots/07-recruit-pro.png)
Upload your requirements and the portal shows the detected column mapping, then lists **Matched Candidates (by Req ID)** so recruiters can see which candidates already belong to which requirement.

### Interview Tracker

![Interview Tracker](docs/screenshots/08-interview-tracker.png)

Note: the Interview Tracker starts empty by design and has its **own** upload button. Its file should contain Candidate Name, Recruiter, Client, Job Role, Interview Date and Interview Status.
Upload interview data to see interview status counts **month-wise** and **day-wise**, overall, by recruiter and by client, plus a custom pivot.

### Monthly Reports

![Monthly Reports](docs/screenshots/09-monthly-reports.png)
A monthly dashboard where you can **Create New Schedule** entries and review monthly activity.

---

## 10. Step 8 — Export and share

Use the export options in the report to download:
- **PDF** snapshots of the dashboard for client or management meetings
- **Excel** versions of tables and pivots for further analysis

---

## 11. Step 9 — Refreshing with new data

Recruiting data changes daily. To update:
1. Update your master workbook (add new rows; keep tab names and headers unchanged).
2. Open **Upload New Data**.
3. Upload the new file and click **Publish to This Report**.

The new upload **replaces** the previous dataset in that browser. Keep your master workbook as the single source of truth.

---

## 12. Data privacy and security — what clients should know

| Topic | Answer |
|---|---|
| Where is my file processed? | In your own browser. It is not sent to a server by this portal. |
| Where is data stored? | In your browser's local storage on your device. |
| Can colleagues see my data? | Not automatically. Each person must upload the file in their own browser. |
| Is login secure? | It is a basic gate only. Use company-level access control for sensitive data. |
| How do I delete my data? | Clear the site's data in your browser settings, or use a private window. |
| Does the portal need internet? | Yes, to load charting and Excel libraries when the page opens. |

**Good practice:** keep candidate files out of public GitHub repositories and email, and share the workbook only with people who need it.

---

## 13. Frequently asked questions

**Can I upload a CSV instead of Excel?** A single-sheet CSV is accepted and treated as the master sheet, but the full multi-tab Excel is recommended to get all modules working.

**Can I upload a Google Sheet directly?** Download it as .xlsx first, then upload.

**Why is a chart empty?** Usually the related column is missing or misspelled. Check the Column Check list.

**Why do numbers differ from my Excel counts?** Check for text dates, duplicate spellings of client/recruiter names, or active filters/date range in the portal.

**My data disappeared.** Data is stored per browser. Private windows, a different browser, a different device or cleared site data will show an empty portal. Upload the workbook again.

**Can two people work on the same data?** Not live. Each person uploads the same workbook in their own browser. A shared database would need a backend (see roadmap).

**Can I rename tabs or columns?** Core tab names and column headers should stay as listed in this guide.

---

## 14. Quick checklist

- [ ] Workbook is .xlsx with tabs: Requirement tracker, INTERVIEW TRACKER STATUS, overall master sheet
- [ ] Headers match the column list; dates are real dates
- [ ] Signed in to the portal
- [ ] Uploaded file; Schema check shows ✓ ✓ ✓
- [ ] Column Check reviewed; Preview numbers look right
- [ ] Clicked **Publish to This Report**
- [ ] Filters set; reports reviewed or exported

---

## 15. Support

For issues, share with your administrator: a screenshot of the Schema check and Column Check, the browser used, and the (non-confidential) file structure. Never send real candidate data over public channels.
