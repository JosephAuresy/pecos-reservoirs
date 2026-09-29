# Water Levels & Storage — Red Bluff Reservoir

**Status: REAL DATA, available now.**

| File | Description |
|---|---|
| `redbluff_storage_water_level_08410000_daily.csv` | Daily water surface elevation (ft), reservoir storage (acre-ft), and percent full |

**Source:** Texas Water Development Board (TWDB), distributed via [waterdatafortexas.org/reservoirs/individual/red-bluff](https://waterdatafortexas.org/reservoirs/individual/red-bluff). Underlying gage: USGS 08410000 "Red Bluff Res nr Orla, TX" (31.90124, -103.91020).

**Coverage:** 1937-02-01 to present (updated daily by TWDB; last refreshed in this repo 2026-09-10). 30,209 days, effectively gap-free.

**Columns:** `date, water_level` (ft, NAVD88-referenced lake datum), `storage_af` = `reservoir_storage` (acre-ft, duplicated column for backward compatibility with existing SWAT+/gwflow calibration scripts), `percent_full` (% of conservation capacity).

**Known facts from this record** (for quick reference, all computed directly from the CSV — not estimates):
- Original conservation capacity (1937): 151,110 acre-ft
- Current conservation capacity (since 2022-09-13): 145,165 acre-ft (TWDB periodically revises the capacity curve as sedimentation surveys are updated)
- Maximum storage ever recorded: 351,000 acre-ft (exceeds conservation capacity — a flood-pool event)
- Minimum storage ever recorded: 10,900 acre-ft
- Mean percent full, last 365 days: ~52%

**Update automation (proposed, not yet implemented):** a small scheduled script (e.g., GitHub Actions cron, daily) pulling `https://waterdatafortexas.org/reservoirs/individual/red-bluff.csv` and committing the refreshed file would keep this current automatically. Not yet wired up — currently a manual pull.

**Recommended use in Delft3D-FM:** water surface elevation time series is the most direct boundary/validation target for a 0-D or fully hydrodynamic reservoir model; convert `water_level` (ft, local lake datum) to your model's vertical datum before use — this file does NOT include a NAVD88-to-local-datum offset, confirm against the site's own datum note if precision matters.
