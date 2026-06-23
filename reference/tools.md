# CarbonInsights MCP — Tools Reference

All tools are **read-only**. Authentication is optional per call when OAuth or env token is configured.

---

## Auth & discovery

### `verify_api_token`

Validate API token and list accessible tables.

| When | First session or auth errors |
| Next | `list_tables` → `analyze_table` |

```json
{}
```

---

### `list_tables`

Discover tables and column schemas for the authenticated user.

| When | Before any data or analysis question |
| Next | `analyze_table` (preferred) or `get_table_structure` |

```json
{}
```

---

### `get_table_structure`

Column names and types for one table.

| When | Need column names before custom `get_table_data` queries |
| Note | `analyze_table` auto-detects columns — prefer it for most questions |

```json
{ "table": "<name from list_tables>" }
```

---

### `suggest_dataset`

Match a user question to the best table **from accessible tables only**.

| When | Vague questions ("power emissions", "maritime costs") |
| Not | A static catalog — only tables assigned to the user's API key |

```json
{ "topic": "power emissions" }
```

Returns: `matches`, `recommendation` (table + `preferred_tool`), `llm_guidance`.

---

### `get_analysis_rules`

Returns the full CarbonInsights LLM playbook (persona + charts + data rules).

| When | Session start, before reports, when unsure how to present data |

```json
{}
```

---

## Analysis (primary)

### `analyze_table` ⭐

**Primary tool** for data analysis, insights, and reports.

**Returns:** Executive summary, Statistics (mean/min/max/median/trend), group breakdown, date coverage, sample rows, LLM instructions.

| When | Trends, patterns, summaries, "what does the data show?" |
| Default | **Latest N rows** by date — omit `from`/`to` for current fundamentals |

```json
{
  "table": "<name from list_tables>",
  "from": "2026-06-01",
  "to": "2026-06-17",
  "group_by": "country_code",
  "limit": 500
}
```

| Param | Notes |
|-------|-------|
| `table` | Required — exact name from `list_tables` |
| `from` / `to` | Only for explicit historical periods |
| `limit` | Default 500; without dates = latest rows |
| `group_by` | e.g. `country_code` — auto-detected if omitted |
| `metrics` | Numeric columns to analyze — auto-detected if omitted |

---

### `executive_briefing` ⭐

Full analysis + polished briefing template. Best for user-facing reports.

**Returns:** Headline metrics, executive summary bullets, statistics, strict presentation rules.

| When | Reports, briefings, stakeholder updates |

```json
{ "table": "<name from list_tables>" }
```

---

### `trader_market_briefing`

Single-dataset EUA trader briefing with chart guidance.

⚠️ **ONE TABLE ONLY.** For full desk across all tables, use `multi_table_desk_briefing`.

| When | Deep-dive on one specific dataset |
| Default | Latest dates — omit `from`/`to` unless user asks for history |

```json
{ "table": "<name from list_tables>" }
```

---

### `multi_table_desk_briefing` ⭐

**Full EUA desk** — orchestrates analysis across every accessible table.

**Returns:**
- `unified_eua_read` — composite bullish/bearish/neutral bias
- `desk_signals` — per-dataset EUA bias, trend, change_pct
- `dataset_summaries` — condensed analysis per table
- `signals_by_domain` — grouped by power, industry, maritime, forecast, market

| When | "Full desk", "all tables", "EUA overview", "market read" |
| Default | Omit `tables` to analyze all accessible datasets |

```json
{}
```

```json
{
  "tables": ["<optional subset from list_tables>"],
  "max_tables": 12
}
```

---

## Domain presets

Auto-select the best matching table from `list_tables`. Optional `table` override.

| Tool | Domain | Example |
|------|--------|---------|
| `analyze_power_emissions` | EU power CO₂ | `{}` or `{ "table": "..." }` |
| `analyze_industry_emissions` | Industry / aviation | `{}` |
| `analyze_forecast` | Europe power forecast | `{}` |
| `analyze_maritime` | Maritime EU ETS trip costs | `{}` |

Shared optional params: `from`, `to`, `limit`, `group_by`.

---

## Comparisons & snapshots

### `compare_periods`

Compare metrics between two custom date ranges.

```json
{
  "table": "<name from list_tables>",
  "period_a_from": "2026-06-01",
  "period_a_to": "2026-06-07",
  "period_b_from": "2026-06-08",
  "period_b_to": "2026-06-17"
}
```

---

### `compare_recent_weeks`

Auto-splits last 14 days into two 7-day periods.

| When | "Week over week", recent change |

```json
{ "table": "<name from list_tables>" }
```

---

### `rank_countries`

Country/segment ranking via `analyze_table` with `group_by`.

| When | "Top emitters", "which country" |

```json
{
  "table": "<name from list_tables>",
  "metric": "total_emissions",
  "group_by": "country_code"
}
```

---

### `get_latest_snapshot`

Most recent rows (sorted by date desc).

| When | "Latest value", "most recent data" |
| Not for | Deep analysis — use `analyze_table` or `executive_briefing` |

```json
{ "table": "<name from list_tables>", "rows": 5 }
```

---

## Low-level data

### `get_table_data`

Raw rows — use `analyze_table` instead for analysis questions.

| When | User explicitly needs raw JSON/CSV, pagination, full export |

```json
{
  "table": "<name from list_tables>",
  "limit": 100,
  "sort": "date",
  "order": "desc",
  "from": "2026-06-01",
  "to": "2026-06-17"
}
```

| Param | Notes |
|-------|-------|
| `limit` | Default API 1000; max 10000 |
| `offset` | Pagination |
| `all` | Full dataset in batches — only when explicitly needed |
| `nocache` | Bypass cache for freshest values |

---

## Advanced desk tools

### `analyze_eua_market`

EUA futures briefing — price momentum, open interest, market read. Auto-resolves market dataset from `list_tables`.

```json
{}
```

---

### `analyze_aviation`

Aviation-only CO₂ and flight trends. Auto-resolves aviation dataset from `list_tables`.

```json
{}
```

---

### `analyze_fuel_switch`

Gas vs coal generation trends and EUA intensity implication.

```json
{}
```

---

### `compare_yoy`

Latest N-day window vs same calendar window one year prior.

```json
{
  "table": "<name from list_tables>",
  "window_days": 7
}
```

---

### `fundamentals_price_read` ⭐

Merge emissions desk + EUA futures — flags alignment/divergence.

```json
{}
```

---

### `desk_alert_scan`

Scan all accessible tables for large % moves (default ≥10%).

```json
{ "threshold_pct": 10 }
```

---

### `get_chart_series`

Structured time-series JSON for charts — exact CarbonInsights points.

```json
{
  "table": "<name from list_tables>",
  "metric": "<column from get_table_structure>",
  "max_points": 60
}
```

---

## Tool workflow summary

| Goal | Tool |
|------|------|
| Pick the right dataset | `suggest_dataset` |
| **Full EUA desk (all tables)** | **`multi_table_desk_briefing`** |
| **Fundamentals vs price** | **`fundamentals_price_read`** |
| **Morning alerts / large moves** | **`desk_alert_scan`** |
| EUA futures / market | `analyze_eua_market` |
| Aviation only | `analyze_aviation` |
| Gas vs coal fuel switch | `analyze_fuel_switch` |
| Year-over-year | `compare_yoy` |
| Chart series (JSON) | `get_chart_series` |
| General analysis | `analyze_table` |
| EU power emissions | `analyze_power_emissions` |
| EU industry / aviation | `analyze_industry_emissions` |
| Power & CO₂ forecast | `analyze_forecast` |
| Maritime EU ETS costs | `analyze_maritime` |
| Country ranking | `rank_countries` |
| Last week vs prior week | `compare_recent_weeks` |
| Latest data point(s) | `get_latest_snapshot` |
| Polished user briefing | `executive_briefing` |
| Single-table EUA briefing | `trader_market_briefing` |
| Two custom date ranges | `compare_periods` |
| Raw export only | `get_table_data` |
| Session rules | `get_analysis_rules` |
