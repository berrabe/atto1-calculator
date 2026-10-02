# Atto 1 Calculator

A tiny EV calculator for the **BYD Atto 1 Dynamic** (2026, CKD Indonesia) — 30.08 kWh, 300 km NEDC, AC 6.6 kW, DC 30 kW.

It answers two questions the car's own UI doesn't:

1. **How much energy, time, and money** does a charge from X% to Y% cost?
2. **How much battery** does a trip of X km consume — and what's left when I arrive?

<div align="center">

| Charge | Trip |
|---|---|
| <img src="assets/screenshot-charge.png" width="270" alt="Charge tab"> | <img src="assets/screenshot-trip.png" width="270" alt="Trip tab"> |

</div>

**Live:** [berrabe.github.io/atto1-calculator](https://berrabe.github.io/atto1-calculator/)

## Install on iPhone

1. Open the live URL in **Safari**
2. Share → **Add to Home Screen**
3. Done — it runs full-screen and works **completely offline** after the first open (service worker)

Also works on any modern browser on desktop/Android.

## What it does

- **Charge** — enter current % and target %: get kWh from the wall (what you pay), kWh into the battery, range gained, estimated time, and cost. Charger type AC (6.6 kW) / DC (30 kW) switches the tariff automatically. DC mode adds PBJT-TL tax and an optional per-session service fee.
- **Trip** — enter distance and current battery %: get energy used, remaining %, remaining range, and a clear *enough / not enough* verdict. Round-trip toggle included.
- Consumption is modeled in **kWh / 100 km** — the same unit the car's trip computer shows. Presets: City 9 · Mixed 11 · Highway 14, or type your own.
- **English / Indonesian** toggle (auto-detects browser language).

## Assumptions & tariff sources

| Item | Default | Source |
|---|---|---|
| Battery | 30.08 kWh | Atto 1 Dynamic spec |
| Range | 300 km NEDC | Factory claim (1% = 3 km) |
| Charging efficiency | ~90% | Wall → battery losses |
| **AC / home tariff** | Rp1.444,70/kWh | PLN R-1/TR 1.300–2.200 VA, Q3 2026 (900 VA: Rp1.352 · 3.500+ VA: Rp1.699,53) |
| **DC / SPKLU tariff** | Rp2.466,78/kWh | ESDM "Layanan Khusus" rate — flat, verified from 6 real PLN invoices (Sep 2026) |
| **PBJT-TL** | 8%, editable | Local electricity tax, varies **0–9%** per region/transaction (observed in the same 6 invoices: 0, 4, 6, 8, 8, 9%) |
| **Service fee/session** | Rp0, hidden by default | PLN SPKLU charges none; third-party operators (Voltron etc.) set their own — tap **+ Service fee** in DC mode |

In-app ⓘ tooltips show the same sources. All numbers are editable — nothing is locked.

## Self-test

Append `?test=1` to run the built-in assertion suite (includes a regression test replaying a real SPKLU invoice: 14.452 kWh @ Rp2.466,78 + 8% PBJT = Rp38.502).

## Tech

- **Two files**: `index.html` (app, ~950 lines) + `sw.js` (offline cache, 24 lines)
- Vanilla HTML/CSS/JS — **zero dependencies, zero build step, no CDN**
- State persists in `localStorage`; works from `file://`, any static host, or GitHub Pages

## Deploy / update

Hosted on GitHub Pages (`main` / root). Deploy = `git push`.

When shipping changes to an already-installed client, bump the `CACHE` version in `sw.js` so the service worker refreshes.

Deep links: `?tab=trip` opens the Trip tab directly · `?test=1` runs the self-test.
