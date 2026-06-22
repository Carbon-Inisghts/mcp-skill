# Daily EUA Desk Brief — Template

Use MCP prompt: `morning-desk-note`

## Tools to call (in order)

1. `desk_alert_scan({ threshold_pct: 10 })`
2. `multi_table_desk_briefing({})`
3. `fundamentals_price_read({})`
4. Optional: `get_chart_series({ table: "ckz_futures_view", metric: "Close" })`

## Output structure

```markdown
## [Headline — composite EUA bias + key alert or price figure]

### Alerts (≥10% moves)
- [table]: [metric] [±X%] — [bearish/bullish EUA]

[Chart: alert bar chart or price line from get_chart_series]

### Fundamentals
- Composite: [neutral/bearish/bullish EUA]
- Power: [figure]
- Industry/aviation: [figure]
- Maritime: [figure]

### Fundamentals vs price
- Divergence: [aligned / divergent / mixed]
- [One sentence on whether EUA price reflects emissions trend]

### EUA implication
[Data-grounded trade-room read — 2–3 sentences]

*Source: CarbonInsights.*
```

## Rules

- CarbonInsights data only — no external figures
- Default to **latest dates** — omit `from`/`to` unless user asks for history
- Always include 1–3 charts
- No disclaimers or hedging
