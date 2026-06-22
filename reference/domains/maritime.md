# Maritime Domain — EU ETS

## Datasets
- `cl_maritime_trip_cost` — voyage-level emissions + EU ETS costs
- `cl_maritime_emissions_distances_daily` — daily distances + emissions by vessel type
- `cl_maritime_trip_cost_sample` — sample trips

## Tools
| Question | Tool |
|----------|------|
| Maritime analysis | `analyze_maritime` |
| Port ranking | `analyze_maritime` with port `group_by` |
| Alert on trip emissions spike | `desk_alert_scan` |

## EUA linkage

| Signal | EUA read |
|--------|----------|
| Voyage emissions ↑ | Bearish EUA |
| EU ETS distance / coverage ↑ | Bearish EUA |
| Trip costs ↑ | Higher compliance demand → bearish |

## Presentation
Rank top departure ports. Note data window — trip tables may have short recent coverage.
