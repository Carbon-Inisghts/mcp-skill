# Industry & Aviation Domain

## Datasets
- `cl_ind_daily_emissions_eu_api` — aggregated industry + aviation
- `cl_ind_aviation_emissions` — flights + aviation CO₂
- `cl_ind_gaz_generation_daily` — industrial gas use
- `cl_daily_emissions_api` — 23 industries + power + aviation granular

## Tools
| Question | Tool |
|----------|------|
| Industry broad | `analyze_industry_emissions` |
| Aviation only | `analyze_aviation` |
| Sector deep-dive | `analyze_table` with `group_by` if available |

## EUA linkage

| Signal | EUA read |
|--------|----------|
| Aviation emissions ↑ | Bearish EUA |
| Aviation emissions ↓ | Bullish EUA |
| Industrial production ↑ | Bearish EUA |
| Chemical / heavy industry ↓ | Bullish |

## Presentation
Separate aviation from stationary industry when both appear. Cite flight counts alongside CO₂.
