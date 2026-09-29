# Satellite Observations — Red Bluff Reservoir

**Status: NOT YET AVAILABLE.** No remote-sensing extraction has been done for Red Bluff Reservoir in this project. This is a genuine, currently-empty gap, not a placeholder for existing work.

## Why it matters
Satellite optical/thermal imagery can supply, at no field cost: reservoir surface area through time (cross-check against the storage/elevation curve in `water_levels/` and help detect bathymetry drift from sedimentation), surface temperature (a real boundary-condition proxy for a thermal/salinity model when no in-situ logger exists), and turbidity/chlorophyll-a proxies from reflectance band ratios (a rough, indirect water-quality indicator — not a substitute for real TDS/conductivity samples, but useful for identifying when/where conditions change between the sparse discrete samples noted in `salinity/`).

## Likely source agencies / platforms
- **USGS/NASA Landsat** (5/7/8/9) — 30 m optical + thermal, 16-day revisit, free via USGS EarthExplorer or Google Earth Engine, record back to the 1980s (matches well with the long water-level record already in `water_levels/`).
- **ESA Sentinel-2** — 10-20 m optical, 5-day revisit (with 2 satellites), since 2015; better spatial/temporal resolution than Landsat but a shorter record.
- **NASA MODIS** — coarser (250 m-1 km) but daily revisit and a long record (2000-present); adequate for surface-area/temperature trend detection, too coarse for a reservoir Red Bluff's size for anything spatially detailed.

## Estimated update frequency
Landsat: 16 days per satellite (8 days with 2 overlapping). Sentinel-2: 5 days. MODIS: daily. All are effectively real-time archives once a processing pipeline exists — no separate "update" step beyond re-running the extraction as new scenes arrive.

## Proposed automation
1. Use Google Earth Engine (free for research/education use) to script a time series of: reservoir surface area (NDWI/MNDWI water mask), surface temperature (Landsat thermal band), and a turbidity proxy (red/NIR reflectance ratio) over the Red Bluff polygon (see `geometry/` for the boundary once available — an interim NHD polygon would work for this purpose).
2. Cross-validate the satellite-derived surface area against the real `water_levels/` storage/elevation record (a large systematic offset would flag either a bad water mask or a genuinely outdated bathymetry/capacity curve).
3. Schedule a periodic (e.g. monthly) re-run once the pipeline exists; no infrastructure currently in place.
