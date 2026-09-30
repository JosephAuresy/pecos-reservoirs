# Outflows / Release — Red Bluff Reservoir

**Status: REAL DATA, partial coverage.**

| File | Description |
|---|---|
| `redbluff_release_daily.csv` | Daily release/outflow, `release_cms` and `release_m3day`, with a `source` flag |

**Coverage:** 2000-01-01 to 2020-12-31 (7,671 days). The `source` column marks whether each day's value came from a real USGS gage reading or a proxy/reconstruction (`USGS_gage_proxy`) — check this column before using a given period for calibration; do not assume every day is an independent field measurement.

**Gap:** unlike storage (now 1937-2026, see `water_levels/`), release/outflow has **not** been extended past 2020. Red Bluff releases serve downstream irrigation districts (Reeves County Water Improvement Canal, Barstow Canal, Giffin Canal, per the companion Reuse Lab's canal-network layer) — a modern release record (2021-present) likely exists via the same district/TCEQ/TWDB reporting chain that produced the original file, but has not been re-pulled for this Hub.

**Recommended next step:** identify the original source/agency for `obs_release_RedBluff.csv` (documented in the parent SWAT+/gwflow project, not re-derived here) and re-run the same extraction through the present. If it turns out to trace back to a USGS gage with a `dv` service (like 08407500/08408500 above), the same NWIS pull pattern used for `inflows/` applies directly.

**Recommended use in a hydrodynamic/water-quality model:** outflow is a direct discharge boundary condition at the dam/outlet structure; combine with `water_levels/` and `inflows/` for a closed water balance check before trusting any of the three in a calibration run.
