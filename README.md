# Pecos Reservoir Management & Reuse Siting Lab

Interactive tool for exploring **where treated produced-water** (or recycled municipal water) **reuse could be
placed** along the Pecos River, and **how changing the way the 5 major dams are operated changes the answer** —
using real observed release and storage records (2000–2020) from Santa Rosa, Sumner (Lake Sumner), Brantley,
Avalon, and Red Bluff, between New Mexico and Texas.

**Live demo:** https://josephauresy.github.io/pecos-reservoirs/
*(enable GitHub Pages: Settings → Pages → Deploy from branch `main` / root)*

Companion to the **[Pecos Salinity Transport Lab](https://josephauresy.github.io/pecos-salinity-lab/)** — separate
repo, separate page, both linked from the [TxPWC Dashboard](https://txpwc-dashboard.streamlit.app/).

## 🌊 New: Red Bluff Reservoir Modeling Hub

**[red-bluff-reservoir-hub.html](https://josephauresy.github.io/pecos-reservoirs/red-bluff-reservoir-hub.html)** — a
dedicated data-readiness resource for anyone building a **Delft3D-FM** hydrodynamic/salinity transport model of Red
Bluff Reservoir specifically (the most saline of the 5 dams, sitting just below the Malaga Bend natural brine
source). Real data, honestly scoped:

- **Real, downloadable now:** water level & storage (USGS 08410000/TWDB, 1937–2026, 30,209 days), Pecos River inflow
  (USGS 08407500, 1937–2026), **Delaware River inflow (USGS 08408500, 1937–2026 — already a map marker on this repo's
  main tool since Aug 2026, but new here as a standalone daily CSV; still not in the SWAT+/gwflow calibration
  package)**, and release/outflow (2000–2020). All under `data/red_bluff/`.
- **Documented gaps, not fake placeholders:** bathymetry & mesh geometry, reservoir-surface meteorological forcing,
  satellite-derived surface area/temperature, and a continuous in-reservoir salinity record are all genuinely missing —
  each gap folder under `data/red_bluff/` explains why it matters, the likely source agency, expected update
  frequency, and a proposed automation plan, rather than a "download" button for data that doesn't exist.
- **Digital Twin roadmap:** a `Digital Twin` tab lays out — as an explicitly-labeled vision, not a built model — how
  this reservoir-scale Hub is meant to connect to the basin-scale SWAT+/GWFLOW model in a 3-level hierarchy
  (Watershed → 5-Reservoir Network → Red Bluff/Delft3D-FM).

Built as a second static HTML page (same vanilla JS/Leaflet/dark-theme style as this repo's main tool — no React/build
step was introduced) so it deploys on GitHub Pages exactly like `index.html` does, with zero new infrastructure.

## What it does

- **Reservoir map** — the 5 real dams at their SWAT+ gwflow coordinates, a draggable candidate reuse-site marker,
  and two *verified* context markers: **Malaga Bend** (documented natural brine source, USGS gage 08406500
  coordinates) and the **Pecos pupfish**'s actual current range (Bitter Lake National Wildlife Refuge, near
  Roswell — the species has been eliminated from the river below Brantley, including the Malaga Bend/Red Bluff
  reach). Popups cite official capacity figures (USACE/Reclamation/TWDB) for every dam.
- **Flow & Management** — a visual river diagram (all 5 dams drawn as one connected line, color/thickness =
  flow) that updates live with a 252-month timeline. Below it: **an editable "what-if" release rule for every
  dam at once** (a release-scale % and a guaranteed minimum-flow floor, laid out in a single table so you can
  compare and combine dams instead of losing track switching one at a time), **5 one-click preset scenarios**
  (e.g. "guarantee minimum flow everywhere," "protect the Avalon→Red Bluff reach"), and a **zoomable history
  chart per dam** — click any dam's node on the river diagram or any of its mini-charts to open a full-size,
  drag-to-zoom, hover-for-exact-values chart.
- **Where to Place Reuse Water** — the same river diagram, now colored green/yellow/red by dilution risk for a
  proposed reuse volume; click any stretch to load it into the detail panel. Shows the month-by-month result and
  a full 2000–2020 frequency histogram of how often that stretch would be risky — and, if you set a custom
  release rule upstream, a direct historical-vs-your-rule comparison.
- **Salinity & Fish** — documents that the Pecos is naturally saline (Rustler/Salado evaporite brine, concentrated
  at Malaga Bend), how that maps to the pupfish's real range contraction, and the historical USGS-documented
  brine-alleviation effort at Malaga Bend — explicitly flagged as *context*, not simulated here.
- **Sources & Method** — full table of USGS/GDROM/TWDB gage IDs, official dam capacities with citations, how the
  raw daily CSVs were aggregated, and how the what-if rule engine works (and why it does **not** use the SWAT+
  model's own uncalibrated internal reservoir objects).

Fully responsive — tested at phone (375px), tablet (768px), and desktop widths; the river diagram has generous
invisible tap targets so dam nodes and reaches are easy to hit on a touchscreen, not just with a mouse.

## Scope note

This lab reasons about **water quantity** (flow/dilution capacity) only. The what-if rule engine is a simple
policy calculator layered on the real observed record (`your_release = max(floor, historical × scale)`) — it does
not simulate reservoir storage, inflow, evaporation, or how the next dam downstream would re-regulate the water.
It does not move salt. That is the job of the companion Salinity Lab (SWAT+/gwflow advection–dispersion). Once the
full Pecos SWAT+/gwflow model is calibrated using these same observed release records as its flow forcing, each
reach's simplified "% of flow" risk indicator here is meant to be replaced by real simulated TDS concentration.

## Running locally

No build step. Serve the folder with any static file server, e.g.:

```
python -m http.server 8732
```

then open `http://localhost:8732/`.

## Structure

- `index.html` — the entire application (HTML/CSS/JS, single file, no external dependencies except Leaflet for the map)

## Data provenance

All release/storage/coordinate data comes from the Pecos_USA SWAT+ gwflow model
(`gwflow/TxtInOut_gwflow/reservoir.con`, `gwflow/input_files/obs_reservoir/*.csv`). Malaga Bend, Pecos pupfish
range, ESA listing status, and dam capacity figures are cited to USGS, USFWS, the Federal Register, and
Wikipedia-sourced USACE/Reclamation/TWDB records — see the in-app **Sources & Method** tab for the full citation
list with links.
