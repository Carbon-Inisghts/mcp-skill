# Market Domain — EUA Futures & Positioning

## Datasets
- `ckz_futures_view` — EUA Dec futures (Close, Open_interest, Volume)
- `COT` — Commitment of Traders positioning

## Tools
| Question | Tool |
|----------|------|
| EUA price / futures | `analyze_eua_market` |
| Fundamentals vs price | `fundamentals_price_read` |
| Positioning only | `analyze_table` on COT |
| Price chart series | `get_chart_series({ table: "ckz_futures_view", metric: "Close" })` |

## EUA linkage

Use **fundamentals_price_read** when the user asks whether EUA price reflects emissions:
- **Aligned:** fundamentals bearish + price rising = trend confirmation
- **Divergent:** fundamentals bearish + price falling = watch catch-up or positioning

## Presentation
Lead with Close trend and % change. Add open interest for positioning context. Never invent prices — use CarbonInsights Close only.
