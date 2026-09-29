# FuelIQ --- Premium Vehicle Management

FuelIQ is a browser-based vehicle management dashboard for tracking
fuel, expenses, trips, efficiency, running costs and vehicle-related
reminders.

**Live demo:** https://biseshkmahato.github.io/Fuel/

------------------------------------------------------------------------

## Features

### 📊 Dashboard & Analytics

-   At-a-glance KPIs for:
    -   Average fuel efficiency
    -   True cost per kilometre
    -   Fuel cost per kilometre
    -   Total distance
    -   Fuel spend
    -   Other expenses
    -   Average fuel price
-   Interactive charts and analytics
-   Time filters:
    -   All Time
    -   This Month
    -   3 Months
    -   6 Months
    -   YTD
    -   12 Months
-   Efficiency and cost analysis
-   Fuel-station spend analysis
-   Expense breakdowns

### ⛽ Fuel Tracking

Record fuel fill-ups with details such as: - Date - Odometer - Litres -
Amount - Fuel price - Fuel station - Vehicle

FuelIQ supports rolling-average efficiency calculations and configurable
efficiency targets.

### 💰 Expense Management

Track non-fuel vehicle expenses such as: - Service and maintenance -
Washing - Tolls - Repairs - Insurance - Other vehicle-related expenses

### 🚘 Multiple Vehicles

-   Add multiple vehicles
-   Switch between vehicles from the dashboard
-   Store vehicle-specific information
-   Set vehicle type and tank capacity
-   Maintain separate logs and analytics

### 🔔 Reminders

Create reminders for: - Service - Insurance - PUC - Custom vehicle tasks

Reminders can optionally include: - Due date - Due odometer

### 🎯 Budget & Efficiency Targets

Configure: - Monthly vehicle budget - Target KMPL - Rolling efficiency
window - Calculation mode - Tank capacity - Vehicle type

FuelIQ uses these settings in the dashboard and monthly reporting.

### ☁️ Google Drive Sync

FuelIQ can sign in with Google and synchronize its data to the user's
own Google Drive.

The application stores its backup as:

`fueliq-data.json`

The Drive integration uses Google's `drive.file` scope so FuelIQ is
designed to access the file it creates rather than the user's entire
Drive.

Data is automatically synchronized after changes, with manual sync
available from the Google Drive settings.

### 📧 Monthly Email Reports

FuelIQ includes a monthly reporting workflow that can send a vehicle
report through Google Apps Script.

The report workflow supports: - Selecting the reporting month -
Selecting a vehicle - Previewing the report - Sending a report
immediately - Connecting the dashboard to an Apps Script Web App -
Automated previous-month reporting through a time-based Apps Script
trigger

The Apps Script backend can generate the monthly email and PDF report.

### 📅 Annual Summary

The dashboard includes a year-in-review summary for the selected
vehicle, with yearly spending, distance and efficiency information where
sufficient data is available.

### 📁 Import / Export

FuelIQ supports: - CSV export - Bulk CSV import - JSON backup - JSON
restore - Print / Save dashboard as PDF

### 🌙 Responsive UI

FuelIQ is designed for desktop, tablet and mobile use.

It includes: - Dark / light mode - Mobile bottom navigation - Responsive
KPI cards - Responsive charts - Touch-friendly controls - Mobile-safe
tables and scrolling - PWA-style mobile metadata

------------------------------------------------------------------------

## Data Storage

FuelIQ uses browser `localStorage` for local application state.

When Google Drive Sync is enabled, the application synchronizes the
FuelIQ dataset to the user's Google Drive as:

``` text
fueliq-data.json
```

This means the dashboard can be used locally without a server, while
Google Drive provides an optional cloud backup and cross-device
synchronization layer.

------------------------------------------------------------------------

## Monthly Email Automation

The monthly email workflow has two parts:

### 1. FuelIQ frontend

The dashboard contains the Monthly Email Report interface.

From:

**Settings → Monthly Email Report**

you can configure: - Report month - Vehicle - Recipient - Apps Script
Web App URL

The frontend can preview the report and send the selected report to the
Apps Script endpoint.

### 2. Google Apps Script backend

The Apps Script project handles: - Reading FuelIQ data - Calculating
monthly metrics - Creating the monthly report - Creating the PDF
attachment - Sending the email - Running the previous-month report
automatically

For automatic reporting, the Apps Script project uses a time-based
trigger for:

``` text
sendPreviousMonthReport
```

A typical schedule is the first day of every month.

For example:

``` text
1 October  → September report
1 November → October report
1 December → November report
```

The Apps Script Web App URL is connected to the FuelIQ dashboard through
the Monthly Email Report settings.

------------------------------------------------------------------------

## Technology

FuelIQ is intentionally lightweight and primarily client-side.

### Core

-   HTML5
-   CSS3
-   JavaScript
-   Browser `localStorage`

### Visualization

-   Chart.js

### Google Integration

-   Google Identity Services
-   Google Drive REST API
-   Google Apps Script
-   Gmail / Apps Script email delivery

### Fonts

-   Chakra Petch
-   DM Sans

The current dashboard loads Chart.js, Google Identity Services and web
fonts from external CDNs/services.

------------------------------------------------------------------------

## Project Structure

The main application is currently contained in:

``` text
index.html
```

The application is designed as a single-page dashboard, with the UI,
styling and JavaScript logic contained in the HTML file.

A separate Google Apps Script project is used for the automated monthly
email/PDF backend.

------------------------------------------------------------------------

## Running Locally

Because FuelIQ is primarily a client-side application, the dashboard can
be opened directly in a browser.

For the best experience, especially with Google authentication and Drive
synchronization, serve it from an authorized HTTPS origin such as GitHub
Pages.

Example:

``` text
https://biseshkmahato.github.io/Fuel/
```

------------------------------------------------------------------------

## GitHub Pages Deployment

1.  Push `index.html` to the repository.
2.  Open the repository's **Settings → Pages**.
3.  Select the deployment branch and folder.
4.  Save the GitHub Pages configuration.
5.  Open the generated Pages URL.

After updating the HTML:

``` bash
git add index.html
git commit -m "Update FuelIQ dashboard"
git push
```

GitHub Pages will publish the updated dashboard.

------------------------------------------------------------------------

## Google Drive Setup

1.  Open FuelIQ.
2.  Click **Sign in with Google**.
3.  Authorize the requested Google permissions.
4.  FuelIQ creates/synchronizes its own `fueliq-data.json` backup.
5.  The signed-in account is shown in the dashboard.

The Google OAuth client must have the deployed website origin authorized
in the corresponding Google Cloud project.

------------------------------------------------------------------------

## Monthly Email Setup

1.  Create/open the Google Apps Script project.
2.  Add the FuelIQ monthly-report backend.
3.  Authorize the script.
4.  Deploy it as a **Web App**.
5.  Set the Web App to execute as the script owner.
6.  Configure access according to your intended use.
7.  Copy the deployed `/exec` URL.
8.  Open FuelIQ → **Settings → Monthly Email Report**.
9.  Paste the Apps Script Web App URL.
10. Select the recipient and report month.
11. Use **Preview** or **Send Now** to test.
12. Configure the Apps Script time-based trigger for automatic monthly
    delivery.

------------------------------------------------------------------------

## Privacy & Data

FuelIQ is designed around user-controlled storage.

-   Dashboard data is stored locally in the browser.
-   Google Drive synchronization stores the FuelIQ backup in the
    signed-in user's Drive.
-   The Drive integration is scoped to the application's Drive file
    access.
-   Monthly email delivery requires the separately configured Apps
    Script backend.
-   The repository does not need a traditional application server for
    normal dashboard operation.

Do not publish private data, API secrets, service-account credentials or
Apps Script credentials in the repository.

------------------------------------------------------------------------

## Backup Recommendation

Even with Google Drive synchronization enabled, periodically export a
JSON backup from:

**Settings → Backup Data (JSON)**

Keep an offline copy if the vehicle history is important to you.

------------------------------------------------------------------------

## Roadmap Ideas

Possible future improvements include:

-   Service-cost forecasting
-   Fuel-price trend alerts
-   Maintenance cost analytics
-   More detailed trip analytics
-   Multi-vehicle comparison dashboards
-   PWA installation/offline enhancements
-   More report customization
-   Additional notification channels

------------------------------------------------------------------------

## License

No license has been specified for this repository yet.

If you want others to freely use, modify and redistribute FuelIQ, add an
appropriate open-source license such as MIT. Otherwise, the repository
remains subject to the default copyright position.

------------------------------------------------------------------------

## Author

**Bisesh Kumar Mahato**

FuelIQ --- Premium Vehicle Management
