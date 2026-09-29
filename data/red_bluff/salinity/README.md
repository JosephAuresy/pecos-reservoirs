# Salinity & Water Quality — Red Bluff Reservoir

**Status: METADATA ONLY in this repository — real historical sample records are documented and citable, but not yet re-extracted into a clean CSV here.**

## What is real and already known
- USGS 08408500 (Delaware River nr Red Bluff, NM) and 08407500 (Pecos River at Red Bluff, NM) both carry **historical discrete water-quality samples** in the USGS NWIS/Water Quality Portal archive, including dissolved solids (parameters 70300/70301), specific conductance (00095), and major ions — sampled intermittently between 1966 and 2011 at the Delaware River site specifically (per the site's own series catalog, `begin_date 1966-08-24`, `end_date 2011-02-01`, ~28-64 samples depending on parameter). These are spot samples, not a continuous record.
- **Malaga Bend**, a well-documented natural brine seep entering the Pecos upstream of Red Bluff (already mapped in the companion Pecos Reservoir Management & Reuse Lab), is the dominant known driver of Red Bluff's reputation as the most saline of the 5 major Pecos reservoirs — this is long-established in TWDB/USGS literature on Pecos River salinity (see `literature/`), not new to this Hub.
- The basin-wide USGS Pecos River Basin Salinity Assessment (Houston et al. 2019, DOI 10.5066/F7DB800T — already used in the companion Reuse Lab, 4,283 real TDS sites basin-wide) very likely includes sample sites at or near Red Bluff itself; this Hub has not yet filtered that release specifically for Red Bluff-area sites.

## Why it matters
Any coupled Delft3D-FM salinity/transport run needs (a) inflow salinity boundary conditions for the Pecos and Delaware arms separately — since Delaware carries brine-influenced water — and (b) in-reservoir calibration targets (ideally a longitudinal or vertical salinity profile, or at minimum a time series at the dam). Neither currently exists as a ready-to-use file here.

## Likely source agencies
- **USGS NWIS / Water Quality Portal** (waterqualitydata.us) — the historical discrete samples noted above; the legacy `nwis/qw` web service used elsewhere in this project has been retired, but the same records are queryable through the modern Water Quality Portal API.
- **USGS ScienceBase** — the Houston et al. 2019 Pecos Basin Salinity Assessment data release (already integrated elsewhere in this project's tools).
- **TCEQ** — Texas Surface Water Quality Monitoring, may hold more recent samples for Red Bluff Reservoir itself (as opposed to the inflow gages).

## Estimated update frequency
Historical/discrete: effectively static once pulled (records end in the early 2010s at the inflow gages). If TCEQ or USGS still samples Red Bluff Reservoir directly, that would be the only realistic source of anything recent — needs to be checked; not confirmed as of this writing.

## Proposed automation
1. Query the Water Quality Portal REST API (`www.waterqualitydata.gov/data/Result/search`) for site IDs `USGS-08407500`, `USGS-08408500`, and any TCEQ station at/near Red Bluff Reservoir, characteristic names `Dissolved solids`, `Specific conductance`, filtered to the Red Bluff area.
2. Filter the existing Houston et al. 2019 ScienceBase release (already fetched live elsewhere in this project) to sites within a small buffer of the reservoir polygon.
3. Combine into a single `redbluff_salinity_samples.csv` with site, date, parameter, value, units — same long-format convention recommended for the rest of this Hub's downloads.
