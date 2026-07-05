# 💧⚡ Utility Tracker

A lightweight, mobile-friendly web app for tracking your water and electricity meter readings, monitoring usage trends, and keeping an eye on costs — all in a single HTML file with no server, no login, and no ads.

---

## Features

- **Meter readings on any date** — log readings as often or as infrequently as you like; the app calculates usage from consecutive readings regardless of the interval
- **Tiered tariff calculator** — configure your municipality's tiered rate structure; costs are calculated accurately across each band
- **Monthly bills log** — record your actual billed amounts; these take priority over estimates in the cost chart
- **Spike alerts** — the dashboard flags unusual usage (20–40%+ above your recent average) so you can investigate early
- **Trends dashboard** — month-over-month usage chart and cost-over-time line graph
- **Excel importer** — import years of historical readings and bills directly from your existing spreadsheet
- **South African Rand (R)** — all costs displayed in ZAR with local number formatting
- **Dark mode** — automatically follows your device's system preference
- **Offline capable** — once loaded, works without an internet connection
- **Private** — all data is stored locally in your browser; nothing is sent to any server

---

## Getting Started

### Option 1 — GitHub Pages (recommended for phone use)

1. [Create a free GitHub account](https://github.com/join) if you don't have one
2. Click **New repository**, name it `utilities`, set it to **Public**, and click **Create repository**
3. Upload `utility-tracker.html` and rename it to `index.html`
4. Go to **Settings → Pages**, set Source to `main` branch, and click **Save**
5. Your app will be live at `https://yourusername.github.io/utilities` within a minute or two

**To add it to your phone's home screen:**
- **Android (Chrome):** open the URL → tap the three-dot menu → *Add to Home screen*
- **iPhone (Safari):** open the URL → tap the Share button → *Add to Home Screen*

It will open full-screen like a native app.

### Option 2 — Open locally

Download `utility-tracker.html` and open it directly in any browser on your computer or phone. No installation required.

---

## How to Use

### Record tab — log your meter readings

Enter your meter readings whenever you take them — weekly is ideal for accurate comparisons, but any frequency works. The app calculates usage as the difference between consecutive readings, regardless of how many days apart they are.

| Field | What to enter |
|---|---|
| Date | The date you took the reading |
| Water meter (kL) | The number shown on your water meter in kilolitres |
| Electricity meter (kWh) | The number shown on your electricity meter in kilowatt-hours |

> **Tip:** You only need to enter the readings you have — if you only have one meter, leave the other blank.

The app calculates usage by subtracting each reading from the previous one, so the first reading you enter establishes a baseline and won't show usage by itself.

---

### Tariffs tab — set up your rate structure

This is where you configure how costs are estimated from your usage.

#### Water tiers

South African municipalities typically charge water on a sliding scale — the more you use, the higher the rate per kilolitre. Many offer a free basic allocation (e.g. the first 6 kL at R 0.00).

To configure:
1. Set the **From** and **To** values (in kL) for each tier
2. Enter the **rate per kL** for that band
3. Leave the **To** field of the last tier blank (it covers everything above)
4. Click **Add tier** to add more bands if needed
5. Click **Save tariffs** when done

Example (City of Cape Town style):

| From | To | Rate |
|---|---|---|
| 0 kL | 6 kL | R 0.00 |
| 6 kL | 10 kL | R 18.50 |
| 10 kL | 15 kL | R 27.00 |
| 15 kL | — | R 36.00 |

#### Electricity tiers

Same structure for electricity (kWh per month). There is also an optional **fixed monthly charge** field for the network/service access fee that appears on your bill regardless of usage.

> **Note:** These rates are used for *estimates* between billing periods. Your actual monthly bill amount (entered in the Bills tab) always takes priority in the cost chart.

Find your current tariff rates on your municipality's website, or read them off your latest bill.

---

### Bills tab — record your actual monthly bills

After you receive your monthly statement, log the actual amounts here. This ensures the cost chart reflects real figures rather than estimates.

1. Select the **month** the bill covers
2. Enter the **water bill amount** in Rand
3. Enter the **electricity bill amount** in Rand
4. Click **Save bill**

Billed amounts override tariff estimates for that month in all charts and metrics.

---

### Dashboard — your usage at a glance

The dashboard has four sections, in order of priority:

**Alerts** — shown at the top. Once you have at least four weeks of readings, the app compares your most recent week against your four-week rolling average:

| Threshold | Alert type |
|---|---|
| More than 40% above average | Red — spike detected |
| 20–40% above average | Amber — above normal |
| More than 20% below average | Green — usage down |
| Within 20% either way | Green — all normal |

**Latest reading** — four metric cards showing your most recent reading interval's water usage (kL), electricity usage (kWh), and the estimated cost of each based on your tariff tiers.

**Month-over-month usage** — a bar/line chart showing water (bars, left axis) and electricity (dashed line, right axis) usage for each month. Useful for spotting seasonal patterns.

**Cost over time** — a line chart of monthly costs. Months where you've entered an actual bill are shown as billed figures; other months show tariff-based estimates.

---

### History tab — reading log, backup, and import

The History tab has three sections:

**Reading history** — a scrollable list of every reading you've entered, newest first. Each entry shows the meter values and the usage since the previous reading in brackets — e.g. `(+4.2)` for water or `(+312)` for electricity.

**Backup & Restore** — export and import your data:

| Button | What it does |
|---|---|
| Export full backup (.json) | Downloads all readings, bills, and tariff settings as a JSON file. Use this for regular backups and to restore on a new device. |
| Export readings as spreadsheet (.csv) | Downloads readings with calculated usage and cost columns, plus a bills section. Opens in Numbers or Excel. |
| Import backup (.json) | Restores a previous JSON backup. Asks for confirmation before overwriting current data. |

**Import from Excel** — import years of historical readings from your existing spreadsheet. See the full instructions in the next section.

---

### Importing historical data from Excel

If you have existing meter readings in an Excel spreadsheet, you can import them directly into the app — no manual re-entry required.

#### What the importer expects

Your spreadsheet must have three separate worksheets:

**Electricity and Water reading sheets** — each must have at least these two columns (column names are not case-sensitive):

| Column | Description |
|---|---|
| `Date` | The date the reading was taken |
| `Meter Reading` | The actual number shown on the meter dial |

Other columns in your sheet (Days, Usage, Daily Average, etc.) are ignored — the app recalculates these itself.

**Bills sheet** — must have at least these columns:

| Column | Description |
|---|---|
| `Bill Month` | The month the bill covers |
| `Water` | The water portion of the bill in Rand |
| `Electricity` | The electricity portion in Rand |

Other columns (Municipal Rates, Refuse, Late payment fee, payment dates, etc.) are ignored.

#### Supported date formats

The importer handles all of the following automatically:

- `dd-mmm-yy` — e.g. `15-Jan-22`
- `dd-mmm-yyyy` — e.g. `15-Jan-2022`
- `mm/dd/yyyy` — e.g. `01/15/2022`
- Excel internal date serial numbers (the actual format Excel stores dates in)

#### How to import

1. Open the app and go to the **History** tab
2. Scroll to the **Import from Excel** card
3. Type in the exact names of your three sheet tabs as they appear in Excel (they are case-sensitive — `Electricity` is not the same as `electricity`)
4. Tap **Choose Excel file** and select your `.xlsx` file
5. The app imports everything and shows a summary, e.g.:
   > ✓ Imported: 156 electricity readings, 156 water readings, 38 bills.
6. The date range of imported data is shown below the summary

If a sheet name is not found, the app will list the sheet names it did find in your file so you can correct the spelling.

#### How imported data is merged

- Dates that already exist in the app are **overwritten** by the imported reading
- Dates in the import that are not yet in the app are **added**
- Bills are merged the same way — imported months overwrite existing ones
- Your tariff settings are not affected by the import

#### After importing

The dashboard will immediately reflect your full history. With three or more years of data you will see:

- Accurate seasonal patterns in the usage chart
- Meaningful spike alert baselines (based on your real historical average)
- A full cost-over-time chart for every month you have bill data

---

## Password Protection

The app is protected by a password screen that appears each time you open a new browser session. The password is verified using **SHA-256 hashing** in the browser — your actual password is never stored anywhere, only its hash.

**Default password:** `UtilityTracker1`

> ⚠️ Change this before you deploy — see instructions below.

Once unlocked, the app stays unlocked for the rest of that browser session. Closing the tab and reopening it, or starting a fresh browser session, will prompt for the password again.

### How to change your password

1. Go to **[emn178.github.io/online-tools/sha256.html](https://emn178.github.io/online-tools/sha256.html)**
2. Type your new password into the input box and copy the SHA-256 hash it generates
3. Open `index.html` in a text editor and find this line near the bottom of the file:
   ```
   const PASSWORD_HASH = '47d7938587104229967ed538ac8586a62dbf9d46a2783e4bfb2506778bf8e586';
   ```
4. Replace the hash string with your new hash (keep the single quotes)
5. Save the file and upload it to GitHub

### Password strength advice

Since the app is hosted publicly on GitHub Pages, anyone who views the page source can see the hash. A weak password (like a single dictionary word or a short number) could be brute-forced. Use a password that is:

- At least 12 characters long
- A mix of upper and lowercase letters and at least one number
- Not a word you use anywhere else

Example of a strong password: `Sandton@Meter24`

### Security limitation

This is client-side password protection — suitable for keeping casual visitors out, but not equivalent to server-side authentication. Do not use this app to store sensitive financial account details or passwords.

---

## Data & Privacy

All data is stored in your browser's **local storage** — it never leaves your device. This means:

- ✅ Works offline after the first load
- ✅ No account or login required
- ⚠️ Clearing your browser data or cache will erase your readings
- ⚠️ Data does not sync automatically between devices

**To back up your data:** open your browser's developer tools (F12), go to *Application → Local Storage*, and copy the values for `ut_readings`, `ut_bills`, and `ut_tariffs`. You can paste these back in if you ever need to restore.

---

## Tips

- **Consistency is key** — try to read your meters on the same day each week (e.g. every Sunday morning) for the most accurate week-over-week comparisons
- **Set your tariffs first** — do this before you start entering readings so cost estimates are available from the start
- **Log your bill the day it arrives** — the sooner you enter it, the more accurate your cost chart becomes
- **Investigate spikes promptly** — a red water alert could indicate a leak; a red electricity alert might point to a geyser fault or an appliance left on

---

## Requirements

Any modern browser — Chrome, Safari, Firefox, or Edge. No internet connection required after the first load (if hosted on GitHub Pages, the initial load requires connectivity).

---

## License

This project is released for personal use. Feel free to modify the HTML file to suit your needs — for example, to change the currency symbol, adjust the default tariff tiers, or add additional meters.
