# Indicators Domain — ML Trading Signals

CarbonInsights **trading indicators** are ML pipelines that publish directional signals to result datasets in Supabase.

> **Never hardcode table names.** Each API key sees only its assigned tables. Use `list_tables` → `indicator_products`, `catalog`, or `suggest_dataset`.

## Product catalog

| Product | Schedule | Horizon | Find dataset |
|---------|----------|---------|--------------|
| Regime-based technical | Daily post-close | Next-day CKZ direction | `list_tables` / `suggest_dataset({ topic: "regime indicator" })` |
| Auctions intraday | ~3×/week ~11:00 UTC | Same-day close vs h3 | `list_tables` / `suggest_dataset({ topic: "auction intraday" })` |
| COT intraday | Wednesdays 11:00 EU | Same-day close vs h3 | `list_tables` / `suggest_dataset({ topic: "cot intraday" })` |
| Sentiment analysis | Daily 07:40 UTC | News-based verdict | `list_tables` / `suggest_dataset({ topic: "sentiment" })` |

Supporting inputs (auction data, intraday prices, positioning, futures) appear in `list_tables` under market/indicators domains when the client has access.

---

## MCP tools

| Goal | Tool | Params |
|------|------|--------|
| Latest signal | `get_latest_snapshot` | `{ table }` — name from `list_tables` only |
| History, accuracy, probability series | `analyze_table` | `{ table }` — omit dates for latest window |
| Pick dataset | `suggest_dataset` | `{ topic: "regime indicator" }` etc. |
| Signals + fundamentals | `multi_table_desk_briefing` + indicator snapshots | — |
| Positioning context | `suggest_dataset({ topic: "cot positioning" })` → `analyze_table` | — |
| Auction clearing context | `suggest_dataset({ topic: "auction" })` → `analyze_table` | — |

Format responses with [ui-palette.md](../ui-palette.md) (green ↑ / red ↓).

---

## 1. Regime-based technical indicator

**Predicts:** Will CKZ close **higher or lower tomorrow**?

### Five market regimes

| ID | Regime | Rule (first match wins) | Hit rate |
|----|--------|-------------------------|----------|
| 0 | Trending | `\|SMA_5 − SMA_20\| ≥ 1.7` | ~58% |
| 1 | Renewables-driven | renewables_ratio > 0.6 OR 15d corr renewables > 0.5 | ~65% |
| 2 | Fossil-driven | renewables_ratio < 0.4 OR 15d corr fossils > 0.5 | ~65% |
| 3 | Mean-reverting | mean_reversion < 3 AND trend < 3 | ~57% |
| 4 | Neutral | Fallback | ~55–60% |

### Output columns (when present in structure)

- `predicted_signal`: **1** = Up, **0** = Down
- `predicted_probability`: confidence 0–1
- `manual_regime_num`: active regime 0–4
- `close`, `trend`, `volatility`, `renewables`, `fossils`, `target` (actual, updated when known)

**System hit rate:** ~61.5% overall.

### EUA read

Technical **price** bias — pair with fundamentals via `fundamentals_price_read` or `multi_table_desk_briefing`.

---

## 2. Auctions intraday indicator

**Predicts:** After EU auction (~11:00 UTC), will price **rise or fall into close**?

- Target: close > hour-3 close → UP (1)
- **Hit rate:** ~63.4% (Aug 2024+ validation)

---

## 3. COT intraday indicator

**Predicts:** On **Wednesdays at 11:00**, will close be **above hour-3 price**?

- Combines COT positioning with first 3 hours intraday action
- Optimized for **precision** (minimize false UP)
- **Hit rate:** ~68% (2025 + Jan 2026 OOS)

---

## 4. Sentiment analysis

**Answers:** Current EUA **market sentiment** from news?

| Field | Values |
|-------|--------|
| `sentiment` | bullish, bearish, neutral |
| `sentiment_score` | 0–100 |
| `headline`, `analysis` | AI verdict + justification |

### Score bands

| Score | Read |
|-------|------|
| 0–30 | Strong bearish |
| 46–54 | Neutral |
| 70–100 | Strong bullish |

### EUA read

Narrative overlay — cross-check with `multi_table_desk_briefing` and `analyze_eua_market`.

---

## Presentation template

```markdown
## ↑ Up EUA — Regime indicator ([date from tool])

**Signal:** ↑ Up | **Confidence:** 67.2% | **Regime:** Renewables-driven

[Line chart from tool output only]

### EUA implication
[data-grounded read]

*Source: CarbonInsights.*
```

## MCP resources

- `carboninsights://docs/indicators` — product reference (server)
- `carboninsights://docs/ui-palette` — color palette
