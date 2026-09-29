# Meteorological Forcing — Red Bluff Reservoir

**Status: BASIN-WIDE DATA EXISTS in this project (not Red-Bluff-specific), not yet extracted for this Hub.**

## What already exists in this project
The parent SWAT+/gwflow Pecos model already uses real **TerraClimate** data (Abatzoglou et al. 2018, ~4 km resolution, fetched live via OPeNDAP, no login required) for basin-wide precipitation, actual ET, and potential ET — visible in the companion Pecos Reservoir Management & Reuse Lab's ET layer (6,300 grid cells, 2000-2020, ~303 mm/yr precip basin mean). This is real, already-integrated data — just not yet clipped/exported specifically for the Red Bluff Reservoir surface (needed for an open-water evaporation term in a Delft3D-FM run).

## Why it matters
A reservoir hydrodynamic model needs, at minimum, wind speed/direction (drives surface mixing and seiche behavior), air temperature, humidity, solar radiation, and precipitation directly over the water surface — not just basin-averaged values — to close the surface heat and water balance. Open-water evaporative loss at Red Bluff is also a real, non-trivial term in any water-balance check against `water_levels/`, `inflows/`, and `outflows/`.

## Likely source agencies / datasets
- **TerraClimate** (already used basin-wide in this project) — monthly, 4 km, precipitation/ET/temperature; adequate for a first-pass water balance but too coarse in time (monthly) for hydrodynamic forcing.
- **NLDAS-2** (NASA/NOAA, hourly, ~12 km, since 1979) — better temporal resolution for wind/radiation/humidity forcing.
- **gridMET** (University of Idaho, daily, 4 km, since 1979) — an alternative to TerraClimate at daily resolution.
- **NOAA HRRR** (hourly, ~3 km, since 2014 only) — best temporal/spatial resolution but short record; useful for recent/forecast-mode runs, not historical calibration.
- Nearest real surface station: NWS/ASOS at Pecos, TX or Carlsbad, NM airports, for a ground-truth check against any gridded product.

## Estimated update frequency
TerraClimate/gridMET: annual release lag (a year or more behind present). NLDAS-2: near-real-time, updated regularly. HRRR: hourly, near-real-time.

## Proposed automation
1. Point-extract TerraClimate (or gridMET/NLDAS-2, if greater temporal resolution is needed) at the Red Bluff Reservoir centroid using the same OPeNDAP access pattern already working elsewhere in this project — no new infrastructure needed, just a new extraction point and variable set (add wind, radiation, humidity to the existing precip/ET pull).
2. Convert to a Delft3D-FM `.wnd`/`.tem`/`.hum` (or unified `.mdw`/FM external forcing) meteorological forcing file.
3. Schedule a periodic re-pull (matching whichever product's own update cadence) once a specific product is selected.
