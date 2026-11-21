# Expense & Income Monitor (Offline PWA)

This project upgrades the supplied single-file finance tracker while preserving its existing interface and core features.

## Included
- `index.html`: original application plus offline/install support
- `manifest.webmanifest`: Android install metadata
- `sw.js`: service worker that caches the app shell for offline launch
- `icons/`: app icons
- Existing bilingual interface, ETB/USD display, Ethiopian/Gregorian dates, budgets, charts, ledger, CSV and JSON backup/restore

## Run locally
A service worker does not work from a `file://` URL. Serve this folder from localhost:

### Windows PowerShell
1. Install Python if it is not already installed.
2. Open PowerShell in this folder.
3. Run:
   ```powershell
   python -m http.server 8000
   ```
4. On the same computer, open `http://localhost:8000`.

For installation on your Android phone, deploy this folder to an HTTPS host such as GitHub Pages or Vercel. HTTPS is required for service workers outside localhost.

## Install on Android
1. Open the deployed HTTPS address in Chrome.
2. Allow the page to finish loading while online.
3. Use the app's **Install App** prompt if Chrome displays it, or Chrome menu → **Install app** / **Add to Home screen**.
4. Open the installed app once while online so the offline cache is populated.
5. Turn off Wi-Fi and mobile data and test opening it.

## Data storage and safety
- The existing `localStorage` key is preserved to avoid discarding data from the earlier version.
- Every save also writes a secondary on-device IndexedDB snapshot where supported.
- If localStorage is unavailable on a later launch, the app attempts to recover the latest IndexedDB snapshot.
- CSV and JSON export remain available. Export a JSON backup regularly and copy it somewhere safe.
- Browser storage is not a cloud backup. Clearing Chrome/site data, uninstalling the app, or device failure can still cause data loss. Keep external backups.
- Data is not encrypted by this project. Protect the phone with its screen lock and do not share exported backups casually.

## Updating the app
When changing app files, update `CACHE_VERSION` in `sw.js` (for example, `expense-income-pwa-v2`) so installed devices fetch the new app shell after they reconnect.

## Important limitations
- Offline use begins only after the first successful online visit/install and cache.
- The app does not synchronize between devices.
- No bank, Telebirr, CBE, M-Pesa, or payment-provider integration is included. Payment method is a transaction label entered by the user.
- The original app's exchange rate remains manually configured. It does not fetch live exchange rates.
