# Power Domain — Trader Interpretation

## Datasets
- `cl_pow_daily_emissions_eu_api` — daily CO₂ by country
- `cl_power_generation_api` — 15-min fuel mix (gas, coal, nuclear, solar, wind)
- `cl_power_load_api` — demand / load
- `cl_power_generation_load_hourly` — hourly stack

## Tools
| Question | Tool |
|----------|------|
| Power emissions trend | `analyze_power_emissions` |
| Gas vs coal switch | `analyze_fuel_switch` |
| Country ranking | `rank_countries` on power table |
| Week-over-week | `compare_recent_weeks` |
| Chart series | `get_chart_series` |

## EUA linkage

| Signal | EUA read |
|--------|----------|
| Power emissions ↑ | Bearish EUA |
| Power emissions ↓ | Bullish EUA |
| Load ↑ + gas generation ↑ | Near-term bearish |
| Coal ↑, gas ↓ | Watch intensity — often bearish if coal displaces clean stack |
| Solar/wind ↑, fossil ↓ | Bullish |

## Presentation
Lead with country breakdown (DE, PL, FR, IT, ES). Chart: emissions line + fuel-mix grouped bar.
