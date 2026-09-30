# Osaka Air Quality Digital Twin — Art of the Possible (v5)

English / 日本語 · 15 pages · four data options

## Quick start on your desktop (no deployment)
Unzip, keep the folder structure, open `index.html`. Choose **Open-Meteo** or **Blended** at the top — both fetch live data straight from Open-Meteo in the browser (internet needed). **Sample** works offline.

## Data options
| Option | Current values | Desktop file | Needs GitHub |
|---|---|---|---|
| Official | Ministry of the Environment stations (Soramame), collected every 30 min | only if the folder was downloaded after a recent collection run (`data/live.js`) | yes |
| Blended (default) | Official stations + Open-Meteo model points where no station is within 6 km; Open-Meteo forecast corrected by the stations | falls back to Open-Meteo only | for the official part |
| Open-Meteo (EU model) | European Copernicus CAMS model at 38 municipal centre points, past 7 days + next 3 days | yes | no |
| Sample | Built-in snapshot, every value invented | yes (offline) | no |

Why the desktop needed this: browsers block a page opened from a file from reading local JSON files. The twin now also loads data as `.js` bundles (`data/live.js`, `data/sample/sample.js`) and fetches Open-Meteo directly, like the Qatar twin.

## Deploy on GitHub (official live data)
1. Public repository; upload everything including `.github` and `.nojekyll`. Delete any older workflow files from v2/v3.
2. Settings → Actions → General → Workflow permissions → **Read and write**.
3. Settings → Pages → Source: **GitHub Actions**.
4. Actions → **Osaka twin - collect live data and deploy** → **Run workflow**. Log ends with `RESULT mode=official stations=NN history=168h`.

Optional backup: repository secret `WAQI_TOKEN` (free token from aqicn.org).

## Rebuild the sample
`OUT_DIR=data/sample SAMPLE=1 SLEEP_MS=0 node --import ./scripts/sample-mock.mjs scripts/fetch-osaka.mjs`

## Data use
Soramame: MOE, local governments, NIES. JMA: government standard terms. Open-Meteo CC BY 4.0 (CAMS, Copernicus licence). Wikidata CC0. OpenStreetMap ODbL. Maps: Esri (ArcGIS Online) and GSI tiles. No cadastral data.

### Background maps (v5)
Esri satellite, topographic, light grey (default) and streets; GSI pale, standard and aerial photo; CARTO light. The picker sits at the top right of every map.
