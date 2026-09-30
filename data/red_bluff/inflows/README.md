# Inflows — Red Bluff Reservoir

**Status: REAL DATA, two independent USGS gages, available now.**

| File | Gage | Coordinates | Coverage |
|---|---|---|---|
| `pecos_river_at_redbluff_08407500_daily.csv` | USGS 08407500 "Pecos River at Red Bluff, NM" | 32.07519, -104.03944 | 1937-10-01 to present, 32,505 days |
| `delaware_river_nr_redbluff_08408500_daily.csv` | USGS 08408500 "Delaware River nr Red Bluff, NM" | 32.02314, -104.05446 | 1937-10-01 to present, 32,500 days |

Both pulled from USGS NWIS daily-values web service, parameter 00060 (discharge), stat 00003 (mean). Columns: `date, discharge_cfs, discharge_cms`.

**Important caveat (documented in the companion Pecos Reservoir Management & Reuse Lab, carried over here):** gage 08407500 sits **~19 km (12 mi) north of the actual dam** — it is the nearest available continuous Pecos mainstem gage, used as an inflow proxy by this project's own SWAT+/gwflow model, not a gage physically at the reservoir headwater. Ungaged local inflow (direct drainage, minor tributaries) between the gage and the reservoir is not captured by either series.

**Delaware River is a real, separate inflow** joining the Pecos just above Red Bluff Reservoir. It was already added as a map marker on the companion Reuse Lab (August 2026, identified via the Pecos River Compact River Master's accounting report) — but not yet used by the SWAT+/gwflow calibration package, and not previously available as a standalone downloadable daily discharge series. That CSV is what this Hub adds.

**Missing for a defensible hydrodynamic/water-quality inflow boundary:**
- **Ungaged local/direct drainage** between 08407500 and the reservoir headwater — no dedicated gage exists; likely source for an estimate: SWAT+/gwflow's own simulated tributary contribution once the model run covering this reach is finalized, or a drainage-area ratio scaling from 08407500.
- **Inflow water temperature and salinity** (see `salinity/`) — needed to drive a coupled hydrodynamic-salinity model run, not just water balance.

**Update automation (proposed):** USGS NWIS daily-values are updated same-day (provisional) to a few days lag (approved); a scheduled pull (daily or weekly) via the same `waterservices.usgs.gov/nwis/dv` endpoint used to build these files would keep them current. Not yet automated.
