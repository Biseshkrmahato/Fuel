# ⛽ FuelIQ — Premium Vehicle Management

A single-file, installable-feeling web app for tracking fuel and EV charging, running costs and efficiency (KMPL or km/kWh). Built for Indian drivers, with no backend, no account and no build step. Open `index.html` and it works.

**Live app:** https://biseshkrmahato.github.io/Fuel/

---

## ✨ Features

### Efficiency & cost analytics
- **KMPL per fill-up** with two calculation modes: **Rolling Average** (forgiving of partial top-ups) and **Strict Full-Tank**
- Configurable rolling window, personal **target** with an over/under indicator, and outlier flags for suspicious entries
- **True cost per km** (fuel + other expenses) vs. fuel-only cost per km
- Estimated remaining range, fuel-in-tank estimate, next-fill odometer estimate and a live efficiency gauge
- 12+ charts: monthly spend, price trend, city/highway split, efficiency trend, cost/km trend, odometer progress, cumulative spend, yearly ownership cost and more
- Time filters (All Time, This Month, 3 / 6 / 12 Months, YTD) applied to every KPI and chart

### 🔌 Electric vehicle support
- Mark any vehicle as **Electric** when you add it, or switch an existing one from the ⋮ menu → **Vehicle Type**
- The log form becomes a **Charging Session**: Energy Added (kWh), Price per kWh, charging network (Home, Tata Power, Statiq, Ather Grid, ChargeZone, Jio-bp pulse) and charging type (Home AC, Public AC, DC Fast)
- Efficiency is shown in **km/kWh** across the dashboard, gauge, table, charts and annual summary
- The gauge uses a car scale (0–10 km/kWh) and switches to a two-wheeler scale (0–40) when your average is above 10
- Range estimate uses your **Battery Capacity** (kWh)
- Each EV keeps its own km/kWh target, separate from your petrol KMPL target
- The receipt scanner is hidden for EVs, since it only reads fuel-pump bills

> Switching an existing vehicle between fuel and electric does **not** convert old entries (litres are not turned into kWh), and its tank/battery capacity and target are cleared.

### Logging
- Three entry types: **Fuel / Charging**, **Other Expense** (Service, Repair, Insurance, Toll, Wash, Accessories, Fine…) and **Trip**
- Fuel types: Petrol, Diesel, Premium and CNG, with Indian station presets (BPCL, IOCL, HPCL, Jio-bp, Shell, Essar / Nayara)
- **Receipt scanning (OCR)** with Tesseract.js, loaded only when you first scan; reads date, litres, rate, amount, station and fuel type
- Odometer sanity checks that warn about likely typos before saving
- Edit or delete any entry, search the log, bulk **CSV import** and CSV export

### Planning & alerts
- Service, insurance and PUC **reminders** by due date or odometer, with "Mark done"
- Monthly budget alerts and tank/battery capacity per vehicle
- **Annual summary** report and a print-friendly dashboard

### Multi-vehicle
- Switch vehicles from the header; entries, reminders, capacity, budget and targets are kept per vehicle
- A comparison dashboard appears once you have two or more vehicles
- **Delete a vehicle** from ⋮ → **Delete Current Vehicle**. The prompt shows how many entries and reminders will be removed. You can't delete your only vehicle. Use **Backup Data (JSON)** first if you might want it back

### Backup & sync
- One-tap **JSON backup / restore**
- Optional **Google Drive sync**: sign in once, changes upload automatically a couple of seconds after each edit, the app reconnects silently on later visits, and it detects newer data from another device. Pull-to-refresh on mobile

### Designed for every screen
- Native-style bottom tab bar on phones and tablets, 2-column KPI grid on phones
- Multi-column layouts on tablet and a wide layout on desktop
- Dark / light theme, safe-area support for notched phones, keyboard focus rings, Escape-to-close
- Add it to your home screen for an app-like experience

---

## 🚀 Getting started

### Just use it
Open the live app above. Your data stays in your browser, so nothing needs to be set up.

### Run locally
No install or build step:

```bash
git clone https://github.com/biseshkrmahato/Fuel.git
cd Fuel
open index.html        # macOS (xdg-open on Linux, or double-click on Windows)
```

### Host your own copy on GitHub Pages
1. Fork this repo, or push `index.html` to a new one.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, pick `main` and `/ (root)`, then **Save**.
4. Your app will be live at `https://<your-username>.github.io/<your-repo>/`.

> Google Drive sign-in only works from origins registered on the OAuth client. If you host your own copy, see the next section.

### Install on your phone
- **Android (Chrome):** menu ⋮ → **Add to Home screen**
- **iOS (Safari):** Share → **Add to Home Screen**

---

## ☁️ Google Drive sync

**Using the live app:** open ⋮ → **Google Drive Sync** → **Sign in with Google**. There is nothing to configure. Your data is saved as one file, `fueliq-data.json`, in your own Drive.

**What it can access:** storage uses the `drive.file` scope, so FuelIQ can only see the file it created, nothing else in your Drive. It also reads your basic Google profile (name, email, photo) to show who is signed in.

### Self-hosting: use your own OAuth client
The Client ID in the source is tied to the original site's URL. If you host a fork elsewhere, create your own:

1. Open the [Google Cloud Console](https://console.cloud.google.com/) and create (or pick) a project.
2. **APIs & Services → Library** → enable the **Google Drive API**.
3. **APIs & Services → OAuth consent screen** → configure it (External is fine) and add yourself as a test user.
4. **Credentials → Create credentials → OAuth client ID** → type **Web application**.
5. Under **Authorized JavaScript origins**, add the exact origin your app is served from, e.g. `https://<your-username>.github.io` (no trailing slash or path).
6. Copy the **Client ID** and replace the `GDRIVE_CLIENT_ID` constant near the top of the Drive section in `index.html`.

> Google occasionally needs a manual sign-in tap (for example if your session has expired or your browser blocks silent sign-in). The Sign in button in the header is always there as a fallback.

---

## 🔒 Privacy & data

- Everything is stored in your browser's **localStorage** on your device. There is no server and no analytics.
- Google Drive sync is opt-in and goes directly from your browser to your own Drive.
- Receipt OCR runs **in the browser**, so images are not uploaded anywhere.
- Clearing your browser data removes local entries. Use **Backup Data (JSON)** or Drive sync regularly.

---

## 🛠️ Tech stack

| | |
|---|---|
| App | Vanilla HTML, CSS and JavaScript in one self-contained file |
| Charts | [Chart.js 4](https://www.chartjs.org/) (CDN) |
| OCR | [Tesseract.js 5](https://tesseract.projectnaptha.com/) (CDN, lazy-loaded) |
| Auth & sync | Google Identity Services + Drive API v3 |
| Storage | Browser `localStorage` (+ optional Drive JSON file) |
| Fonts | Chakra Petch, DM Sans (Google Fonts) |

External scripts load from CDNs, so the first load needs an internet connection.

---

## 📁 Project structure

```
.
├── index.html   # the entire app
├── LICENSE
└── README.md
```

---

## 🧭 Roadmap ideas

- Offline support via a service worker
- Swipe gestures on log rows
- Charging-session cost split for home tariffs (time-of-day rates)
- Chart tap-to-inspect tooltips on mobile

---

## 🤝 Contributing

Issues and pull requests are welcome. Because the app is one file, please keep changes self-contained and test on a phone-sized viewport as well as desktop.

## 📄 License

Released under the [MIT License](LICENSE).
