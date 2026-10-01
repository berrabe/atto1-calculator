# Atto 1 Calculator

Small EV calculator for the **BYD Atto 1 Dynamic (2026, CKD Indonesia)** — 30.08 kWh, 300 km NEDC, AC 6.6 kW, DC 30 kW.

Two calculators:

- **Charge** — how many kWh (and Rupiah) to go from current battery % to a target %, plus estimated charging time and range gained.
- **Trip** — for a trip of X km, how much battery is used and what % / range remains. Round-trip toggle included.

Consumption is modeled in `kWh / 100 km` (the same unit the car's trip computer shows). Presets: City 9, Mixed 11, Highway 14 — or type your own.

## Usage

Open <https://berrabe.github.io/atto1-calculator/> on iPhone → Share → **Add to Home Screen**. It runs standalone (full screen) and works fully offline after the first open (service worker cache).

## Self-test

Append `?test=1` to the URL to run the built-in math assertions (pass/fail banner at the bottom).

## Notes

- Charging assumes ~90% wall-to-battery efficiency.
- DC charging time is a flat estimate — real DC charging tapers near 100%.
- Tariff defaults to PLN home tariff (~Rp1.444,7/kWh), editable in the app.
- To ship an update: bump `CACHE` version in `sw.js` so clients pick up the new files.

## Deploy

GitHub Pages, served from `main` / root. Deploy = `git push`.
