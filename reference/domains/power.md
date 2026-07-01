# Power Domain — Trader Interpretation

## Datasets (discover via `list_tables`)

- Daily power CO₂ by country
- High-frequency generation / fuel mix (gas, coal, nuclear, solar, wind)
- Electricity load / demand
- Hourly generation + load stack
- Power and CO₂ forecasts

Use `suggest_dataset({ topic: "power emissions" })` or `analyze_power_emissions({})` to auto-select from accessible tables.

## Tools

| Question | Tool |
|----------|------|
| Power emissions trend | `analyze_power_emissions` |
| Gas vs coal switch | `analyze_fuel_switch` |
| Country ranking | `rank_countries` (power dataset from `list_tables`) |
| Week-over-week | `compare_recent_weeks` |
| Chart series | `get_chart_series` |

## EUA linkage (price lens)

| Signal | EUA price read |
|--------|----------------|
| Power emissions ↑ | **Bullish** EUA |
| Power emissions ↓ | **Bearish** EUA |
| Load ↑ + gas generation ↑ | Near-term **bullish** |
| Coal ↑, gas ↓ | Watch intensity — often **bullish** if coal displaces clean stack |
| Solar/wind ↑, fossil ↓ | **Bearish** (displaces fossil burn) |

## Presentation

Lead with country breakdown (DE, PL, FR, IT, ES). Chart: emissions line + fuel-mix grouped bar.
