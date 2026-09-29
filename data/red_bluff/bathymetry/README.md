# Bathymetry & Geometry — Red Bluff Reservoir

**Status: NOT YET AVAILABLE in this repository.** No bathymetric survey grid or reservoir mesh geometry is currently included. This folder documents the gap rather than offering a placeholder file.

## Why it matters
A Delft3D-FM (or any hydrodynamic/salinity transport) model needs an actual bed elevation grid — not just surface area vs. storage curves — to build its unstructured mesh, set initial wet/dry cells, and get residence-time and stratification behavior right. Reservoir bathymetry also directly determines the elevation-area-capacity curve TWDB uses to convert Red Bluff's measured water level into the storage/percent-full numbers in `water_levels/` — so a stale bathymetry indirectly biases the storage record too (sedimentation reduces both).

## What partial information already exists
- `conservation_capacity` in `water_levels/redbluff_storage_water_level_08410000_daily.csv` has already dropped from 151,110 acre-ft (1937) to 145,165 acre-ft (since 2022) — TWDB's own periodic capacity-curve updates are themselves indirect evidence of resurveys, even though the underlying grid isn't published in that CSV.
- Approximate dam/pool coordinates and a rough reservoir footprint can be traced from public GIS layers (NHD waterbody polygon, TWDB GIS viewer) — usable for a first-pass map outline, not for meshing.

## Likely source agencies
- **TWDB Hydrographic Survey Program** — periodically resurveys major Texas reservoirs by sonar/GPS, publishing volumetric (elevation-capacity) tables and, for some reservoirs, full survey point clouds. Whether Red Bluff has a recent (post-2010) full-resolution survey on file needs to be checked directly with TWDB.
- **USACE / USBR** — Red Bluff was built and is still nominally under Bureau of Reclamation compact oversight (Red Bluff Water Power Control District); older as-built and survey drawings may exist in USBR/USACE archives.
- **USGS 3DEP / lidar** — bare-earth lidar covers the exposed reservoir margins at low pool but not the submerged bed.

## Estimated update frequency
Full hydrographic resurveys of Texas reservoirs are typically done on a multi-year to multi-decade cycle (driven by budget and sedimentation concerns), not annually. A capacity-curve revision (like the 2022 one visible in the storage data) does not necessarily imply a new public survey grid was released the same year.

## Proposed automation
1. Query the TWDB Hydrographic Survey Program's public survey inventory/GIS index for "Red Bluff Reservoir" (manual check first — no confirmed public API for raw survey point clouds as of this writing).
2. If a digital elevation model or survey point cloud is published, script a one-time (not recurring — bathymetry does not change fast enough to warrant automation) download and conversion to a Delft3D-FM-compatible grid (`.xyz` point file or `.asc`/GeoTIFF raster for `grid2fm`/mesh generation tools).
3. Until then, use the elevation-capacity relationship implicit in `water_levels/` (water_level vs. storage_af, both real) as a coarse 1-D proxy for a reservoir-averaged storage model — not a substitute for a true bathymetric mesh.
