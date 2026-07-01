# CarbonInsights — Dataset Catalog

> Datasets are **per API key**. Always call `list_tables` to see names, columns, and access for this user. **Do not guess or hardcode table names** in skill docs or LLM answers — copy from `list_tables` or use domain tools that auto-resolve.

## Power

| Dataset type | Description | Preferred tool | Typical group_by |
|--------------|-------------|----------------|------------------|
| Daily power CO₂ | Country-level power-sector emissions | `analyze_power_emissions` | `country_code` |
| Power generation / fuel mix | Gas, coal, nuclear, renewables (often high frequency) | `analyze_fuel_switch` | `country_code` |
| Power load / demand | Electricity load time series | `analyze_power_emissions` | `country_code` |
| Hourly generation + load | Combined stack views | `analyze_power_emissions` | — |
| Power / CO₂ forecast | Forward outlook | `analyze_forecast` | — |

**Trader read:** Rising power emissions → bearish EUA. Gas↑ coal↓ → watch intensity. Load↑ + gas↑ → near-term bearish.

## Industry & aviation

| Dataset type | Description | Preferred tool | Typical group_by |
|--------------|-------------|----------------|------------------|
| Aggregated industry + aviation | Stationary industry and aviation combined | `analyze_industry_emissions` | — |
| Aviation-only | Flights + aviation CO₂ | `analyze_aviation` | — |
| Industrial gas use | Gas generation by country/sector | `analyze_industry_emissions` | — |
| Granular daily emissions | Multi-sector breakdown (industry sub-sectors, power, aviation) | `analyze_table` | sector column if present |

**Trader read:** Aviation↓ → bearish EUA price. Industry stable → neutral. Aggregate daily emissions↑ → bullish macro signal.

## Maritime

| Dataset type | Description | Preferred tool | Typical group_by |
|--------------|-------------|----------------|------------------|
| Voyage trip costs | Per-voyage emissions + EU ETS costs | `analyze_maritime` | port / route column |
| Sample trip costs | Sample maritime trips | `analyze_maritime` | port / route column |
| Daily maritime distances | Distances + emissions by vessel type | `analyze_maritime` | — |

**Trader read:** Rising voyage emissions / EU ETS costs → bullish EUA price (higher compliance demand).

## Market & positioning

| Dataset type | Description | Preferred tool | Typical group_by |
|--------------|-------------|----------------|------------------|
| EUA futures | Price, open interest, volume | `analyze_eua_market` | — |
| Positioning (e.g. COT) | Commitment of Traders / positioning data | `analyze_table` | — |

**Trader read:** Price momentum + fundamentals divergence = key desk signal. Use `fundamentals_price_read`.

## Trading indicators (ML signals)

> Use `list_tables` → `indicator_products` for **this** API key. Never hardcode result table names. Playbook: [domains/indicators.md](domains/indicators.md).

| Indicator | Schedule | Tool (latest) | Tool (history) |
|-----------|----------|---------------|----------------|
| Regime technical | Daily | `get_latest_snapshot` | `analyze_table` |
| Auctions intraday | ~3×/week 11:00 UTC | `get_latest_snapshot` | `analyze_table` |
| COT intraday | Wed 11:00 | `get_latest_snapshot` | `analyze_table` |
| Sentiment | Daily 07:40 UTC | `get_latest_snapshot` | `analyze_table` |

Format with [ui-palette.md](../ui-palette.md) — green ↑ / red ↓.

## Forecast evaluation

| Dataset type | Description | Preferred tool | Typical group_by |
|--------------|-------------|----------------|------------------|
| Forecast backtest / accuracy | Model evaluation metrics | `analyze_forecast` | — |

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
| Which dataset? | `suggest_dataset` then `list_tables` |
