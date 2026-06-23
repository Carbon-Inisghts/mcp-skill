# Industry & Aviation Domain

## Datasets (discover via `list_tables`)

- Aggregated stationary industry + aviation
- Aviation-only emissions and flight counts
- Industrial gas use by country/sector
- Granular multi-sector daily emissions (industry sub-sectors, power, aviation)

Use `analyze_industry_emissions`, `analyze_aviation`, or `suggest_dataset` — do not hardcode table names.

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
