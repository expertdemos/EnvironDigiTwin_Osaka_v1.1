# Osaka Air Quality Digital Twin — Art of the Possible (v11)

English / 日本語 · 16 pages · four data options · six pollutants (PM2.5, NO₂, Ox, SO₂, CO, SPM)

## Folder contents
| File / folder | Purpose |
|---|---|
| `index.html` | The page (styles + loader) |
| `app-core.js` | Data loading, calculations, maps, shared components |
| `app-pages.js` | The 15 core pages |
| `app-advisory.js` | Public Advisory page, auto-share simulation, alert ticker, data-freshness panel |
| `app-explain.js` | Floating key for M/C/F/R/A, hover explanations, chart captions, glossary |
| `scripts/fetch-osaka.mjs` | Collector for official data (runs on GitHub every 30 min, or locally) |
| `scripts/sample-mock.mjs` | Builds the offline sample dataset only |
| `.github/workflows/osaka-twin.yml` | GitHub Action: collect + deploy |
| `data/latest.json` | Seed file, replaced on the first successful collection |
| `data/sample/` | Offline sample (every value invented) |
| `.nojekyll` | Required for GitHub Pages |

## Quick start on your desktop
Unzip, keep the folder structure, open `index.html`. **Open-Meteo** and **Blended** fetch live European model data in the browser (internet needed). **Official** shows Open-Meteo with a banner until official data has been collected. **Sample** works offline.

## Deploy on GitHub (official live data)
1. Public repository; upload everything, including `.github` and `.nojekyll`.
2. Settings → Actions → General → Workflow permissions → **Read and write**.
3. Settings → Pages → Source: **GitHub Actions**.
4. Actions → **Osaka twin - collect live data and deploy** → **Run workflow**. The log should end with `RESULT mode=official stations=NN history=168h`.
5. On the site: Data & Method → **Run feed test**.

Optional backup: repository secret `WAQI_TOKEN` (free token from aqicn.org).

## Run the collector on your own computer (optional)
Needs Node.js 20+. In this folder: `node scripts/fetch-osaka.mjs`. It writes `data/live.js`, which the page reads even when opened from a desktop.

## Rebuild the sample
`OUT_DIR=data/sample SAMPLE=1 SLEEP_MS=0 node --import ./scripts/sample-mock.mjs scripts/fetch-osaka.mjs`

## What changed in v11
- Floating key for the letters beside numbers (M measured · C calculated · F model or forecast · R reference · A assumption); appears whenever any are on screen and lists only those visible.
- Every pollutant, unit, abbreviation, technical term, badge, table header and KPI tile has a hover explanation (dotted underline).
- Captions or keys added to every chart and coloured element: hour-of-day bars, pollution rose, regional/urban/roadside bars, forecast range bars, change map, alert and feed colour bars.
- Map key now covers marker shapes, live pulsing, wind arrows, hospitals, the low emission zone, the zoom box and the estimated shading.
- Glossary button (bottom left) with search, and an A–Z glossary on Data & Method.
- Includes v10: Official falls back to live Open-Meteo (not the sample) when no collected data is available; Open-Meteo reuse for 25 min and 30-min refresh; only live official stations pulse; larger markers.

## Data use
Soramame: MOE, local governments, NIES. JMA: government standard terms. Open-Meteo CC BY 4.0 (CAMS, Copernicus licence). Wikidata CC0. OpenStreetMap ODbL. Maps: Esri (ArcGIS Online) and GSI tiles. No cadastral data.
