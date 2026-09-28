# ⛽ FuelIQ — Premium Vehicle Management

A single-file, installable-feeling web app for tracking fuel fill-ups, running costs and mileage (KMPL) — built for Indian drivers, with no backend, no account and no build step. Open `index.html` and it works.

**Live demo:** https://biseshkrmahato.github.io/Fuel/

---

## ✨ Features

**Fuel & mileage analytics**
- KMPL per fill-up with two calculation modes: **Rolling Average** (forgiving of partial top-ups) and **Strict Full-Tank**
- Configurable rolling window, target KMPL with over/under indicator, and outlier flags for suspicious entries
- True cost per km (fuel + other expenses) vs. fuel-only cost per km
- Estimated remaining range, fuel-in-tank estimate and a live efficiency gauge
- Time filters: All Time, This Month, 3 / 6 / 12 Months, YTD — applied to every KPI and chart

**Logging**
- Three entry types: **Fuel**, **Other Expense** (Service, Repair, Insurance, PUC, Toll, Wash, Accessories, Fine…) and **Trip**
- Fuel types: Petrol, Diesel, CNG, EV, Premium — with Indian station presets (IOCL, BPCL, HPCL, Jio-bp, Shell, Essar)
- **Receipt scanning (OCR)** with Tesseract.js — lazy-loaded only when you first scan
- Edit / delete any entry, bulk **CSV import**, CSV export

**Planning & alerts**
- Service / document **reminders** with "Mark done"
- Monthly budget tracking and tank-capacity settings per vehicle
- **Annual summary** report and print-friendly dashboard

**Multi-vehicle** — switch between vehicles from the header; data and settings are kept per vehicle.

**Backup & sync**
- One-tap **JSON backup / restore**
- Optional **automatic Google Drive sync** (see below): silent reconnect on open, debounced auto-save after each change, cross-device change detection, pull-to-refresh on mobile

**Designed for every screen**
- Native-style bottom tab bar on phones and tablets, 2-column KPI grid on phones
- Multi-column layouts on tablet, wide-monitor layout on desktop
- Dark / light theme, safe-area support for notched phones, keyboard focus rings, Escape-to-close
- Add it to your home screen for an app-like experience (includes a home-screen icon)

---

## 🚀 Getting started

### Run locally
No install needed:

```bash
git clone https://github.com/Biseshkrmahato/Fuel
cd Biseshkrmahato/Fuel
# just open the file in a browser
open index.html        # macOS  (use xdg-open on Linux, or double-click on Windows)
```

> Rename `fueliq.html` to `index.html` if you want GitHub Pages to serve it at the root.

### Host on GitHub Pages
1. Push the file to your repo (as `index.html`).
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, pick `main` and `/ (root)`, then **Save**.
4. Your app will be live at `(https://github.com/Biseshkrmahato/Fuel/)

### Install on your phone
- **Android (Chrome):** menu ⋮ → **Add to Home screen**
- **iOS (Safari):** Share → **Add to Home Screen**

---

## ☁️ Google Drive sync setup (optional)

Sync stores one file, `fueliq-data.json`, in your own Google Drive. FuelIQ only requests the `drive.file` scope, meaning it can access **only files it created** — nothing else in your Drive.

1. Open the [Google Cloud Console](https://console.cloud.google.com/) and create (or pick) a project.
2. **APIs & Services → Library** → enable the **Google Drive API**.
3. **APIs & Services → OAuth consent screen** → configure it (External is fine) and add yourself as a test user.
4. **Credentials → Create credentials → OAuth client ID** → type **Web application**.
5. Under **Authorized JavaScript origins**, add the exact URL your app is served from, e.g. `https://<your-username>.github.io` (no trailing slash or path). The app shows your current origin inside the sync dialog.
6. Copy the **Client ID**.
7. In FuelIQ: **⋮ menu → Google Drive Sync** → paste the Client ID → **Connect / Sign in with Google**.

Once connected, changes upload automatically a couple of seconds after you make them, the app reconnects silently on later visits, and it offers to pull down newer data if you edited from another device.

> **Note:** Google occasionally requires a manual sign-in tap (for example if your Google session has expired or your browser blocks silent sign-in). The Sign in button in the header is always there as a fallback.

---

## 🔒 Privacy & data

- Everything is stored in your browser's **localStorage** on your device. There is no server and no analytics.
- Google Drive sync is opt-in and goes directly from your browser to your own Drive.
- Receipt OCR runs **in the browser** — images are not uploaded anywhere.
- Clearing your browser data removes local entries, so use **Backup Data (JSON)** or Drive sync regularly.

---

## 🛠️ Tech stack

| | |
|---|---|
| App | Vanilla HTML, CSS and JavaScript — one self-contained file |
| Charts | [Chart.js 4](https://www.chartjs.org/) (CDN) |
| OCR | [Tesseract.js 5](https://tesseract.projectnaptha.com/) (CDN, lazy-loaded) |
| Auth & sync | Google Identity Services + Drive API v3 |
| Storage | Browser `localStorage` (+ optional Drive JSON file) |

External scripts load from CDNs, so the first load needs an internet connection.

---

## 📁 Project structure

```
.
├── index.html   # the entire app (rename from fueliq.html)
└── README.md
```

---

## 🧭 Roadmap ideas

- Offline support via a service worker
- Swipe gestures on log rows
- Line-icon theme toggle and further icon polish
- Chart tap-to-inspect tooltips on mobile

---

## 🤝 Contributing

Issues and pull requests are welcome. Because the app is one file, please keep changes self-contained and test on a phone-sized viewport as well as desktop.

## 📄 License

[MIT](https://choosealicense.com/licenses/mit/)).
