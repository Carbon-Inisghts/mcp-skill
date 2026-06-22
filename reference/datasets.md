# CarbonInsights — Dataset Catalog

> Tables are **per API key**. Always call `list_tables` to confirm access before analysis.

## Power

| Table | Description | Preferred tool | group_by |
|-------|-------------|----------------|----------|
| `cl_pow_daily_emissions_eu_api` | Daily power CO₂ — IT, DE, FR, ES, PL + EU aggregate | `analyze_power_emissions` | `country_code` |
| `cl_power_generation_api` | 15-min generation by fuel (gas, coal, nuclear, renewables) | `analyze_fuel_switch` | `country_code` |
| `cl_power_load_api` | 15-min electricity load / demand | `analyze_power_emissions` | `country_code` |
| `cl_power_generation_load_hourly` | Hourly generation + load stack | `analyze_power_emissions` | — |
| `europePowerForecast` | Forward power / CO₂ outlook | `analyze_forecast` | — |

**Trader read:** Rising power emissions → bearish EUA. Gas↑ coal↓ → watch intensity. Load↑ + gas↑ → near-term bearish.

## Industry & aviation

| Table | Description | Preferred tool | group_by |
|-------|-------------|----------------|----------|
| `cl_ind_daily_emissions_eu_api` | Aggregated stationary industry + aviation | `analyze_industry_emissions` | — |
| `cl_ind_aviation_emissions` | EU ETS aviation CO₂ + flight counts | `analyze_aviation` | — |
| `cl_ind_gaz_generation_daily` | Daily gas generation by country/sector | `analyze_industry_emissions` | — |
| `cl_daily_emissions_api` | Granular daily emissions (23 industries + power + aviation) | `analyze_table` | — |

**Trader read:** Aviation↓ → bullish EUA. Industry stable → neutral. Aggregate daily emissions↑ → bearish macro signal.

## Maritime

| Table | Description | Preferred tool | group_by |
|-------|-------------|----------------|----------|
| `cl_maritime_trip_cost` | Per-voyage emissions + EU ETS costs (from Feb 2026) | `analyze_maritime` | `departure_port_code` |
| `cl_maritime_trip_cost_sample` | Sample maritime trip costs | `analyze_maritime` | `departure_port_code` |
| `cl_maritime_emissions_distances_daily` | Daily distances + emissions by ship type | `analyze_maritime` | — |

**Trader read:** Rising voyage emissions / EU ETS costs → bearish EUA (higher compliance demand).

## Market & positioning

| Table | Description | Preferred tool | group_by |
|-------|-------------|----------------|----------|
| `ckz_futures_view` | Rolling EUA December futures (Close, OI, volume) | `analyze_eua_market` | — |
| `COT` | Commitment of Traders positioning data | `analyze_table` | — |

**Trader read:** Price momentum + fundamentals divergence = key desk signal. Use `fundamentals_price_read`.

## Forecast evaluation

| Table | Description | Preferred tool | group_by |
|-------|-------------|----------------|----------|
| `cpf_eur_weekly_aggregated_evaluation_api` | Forecast backtest / accuracy metrics | `analyze_forecast` | — |

## Tool selection by question

| User asks | Tool |
|-----------|------|
| Full desk | `multi_table_desk_briefing` |
| What moved / alerts | `desk_alert_scan` |
| Fundamentals vs price | `fundamentals_price_read` |
| EUA futures price | `analyze_eua_market` |
| Gas vs coal | `analyze_fuel_switch` |
| Aviation only | `analyze_aviation` |
| YoY comparison | `compare_yoy` |
| Chart data (exact points) | `get_chart_series` |
