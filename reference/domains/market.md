# Market Domain — EUA Futures & Positioning

## Datasets (discover via `list_tables`)

- EUA futures (price, open interest, volume)
- Positioning data (e.g. commitment of traders)

Use `analyze_eua_market({})` for futures; `analyze_table` for positioning datasets returned by `list_tables`.

## Tools

| Question | Tool |
|----------|------|
| EUA price / futures | `analyze_eua_market` |
| Fundamentals vs price | `fundamentals_price_read` |
| Positioning only | `analyze_table` on accessible positioning dataset |
| Price chart series | `get_chart_series` — `table` and `metric` from `list_tables` / tool output |
| Regime / auction / COT / sentiment signal | `get_latest_snapshot` on results table — see [indicators.md](indicators.md) |
| Signal history / accuracy | `analyze_table` on indicator results |

## EUA linkage

Use **fundamentals_price_read** when the user asks whether EUA price reflects emissions:

- **Aligned:** fundamentals bearish + price rising = trend confirmation
- **Divergent:** fundamentals bearish + price falling = watch catch-up or positioning

## Presentation

Lead with Close trend and % change. Add open interest for positioning context. Never invent prices — use CarbonInsights Close only.

For ML trading signals (regime, auctions, COT, sentiment), see [indicators.md](indicators.md).
Format direction badges with [ui-palette.md](../ui-palette.md).
