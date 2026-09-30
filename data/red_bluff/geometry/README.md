# Geometry (reservoir boundary, mesh inputs) — Red Bluff Reservoir

**Status: NOT YET AVAILABLE as a modeling-ready file.** The map on the Hub page draws an approximate boundary for visualization only (public NHD/OSM-derived outline) — it is NOT a survey-grade polygon and should not be fed directly into mesh generation.

## Why it matters
a hydrodynamic/water-quality model's unstructured mesh needs a real reservoir boundary polygon (full-pool and/or multiple-stage outlines), inlet/outlet structure locations, and ideally cross-sections near the dam and at the Pecos/Delaware confluence to resolve the actual flow path rather than a generic bathtub shape.

## Likely source agencies
- **USGS National Hydrography Dataset (NHD)** — public waterbody polygon for Red Bluff Reservoir, free, but coarse and single-stage (not multi-elevation).
- **TWDB** — same hydrographic survey program as `bathymetry/`; a proper survey typically comes with a matched boundary/contour set.
- **County/USBR as-built drawings** — for the dam and outlet structure geometry specifically (spillway crest, outlet works invert elevation) needed for the outflow boundary condition in a hydrodynamic/water-quality model.

## Estimated update frequency
Reservoir shoreline geometry changes slowly except after major sedimentation or dredging events; a static polygon refreshed only when a new hydrographic survey is published is adequate — no need for frequent automation.

## Proposed automation
1. One-time pull of the NHD waterbody polygon for Red Bluff (via the USGS National Map / NHDPlus HR download service) as an interim boundary for early-stage meshing.
2. Replace with the TWDB survey-derived boundary once/if obtained (see `bathymetry/`).
3. Manually digitize or request from USBR/TWDB the outlet works and spillway geometry — unlikely to be in any bulk GIS dataset, worth a direct records request.
