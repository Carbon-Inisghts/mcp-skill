# CarbonInsights MCP — Workflows

Step-by-step playbooks for common LLM tasks.

---

## Session bootstrap (mandatory)

```
1. get_analysis_rules()         → load desk policy + skill repo URLs (step 1)
2. list_tables()                → discover datasets for THIS API key (step 2)
   (optional) read carboninsights://docs/skill via MCP resources
3. [Answer user question]       → analysis tools only — never skip to rate data quality
```

**Forbidden before init:** scoring data (7.5/10), "strengths/weaknesses" product reviews, critiquing API freshness/windowing from memory.

If `verify_api_token` fails → guide user to [setup.md](setup.md). Never ask user to paste API key in chat when OAuth is available.

---

## Full EUA desk (default for broad questions)

**Triggers:** "desk report", "EUA overview", "market read", "all tables", "full carbon picture", "what's the EUA fundamental read?"

```
1. multi_table_desk_briefing({})
2. Read unified_eua_read.composite_bias → lead headline
3. For each domain in signals_by_domain:
   - State eua_bias per dataset
   - Cite primary_metric, change_pct, date_range
4. Add 1 chart per major domain (power, industry, forecast)
5. End: Source: CarbonInsights
```

**Do not** substitute `trader_market_briefing` on one table.

---

## Single dataset analysis

**Triggers:** "analyze power emissions", "show me industry data", user names one table

```
1. suggest_dataset({ topic: "..." })     → if table unknown
   OR list_tables()                      → if need full list
2. Use recommendation.preferred_tool:
   - analyze_power_emissions
   - analyze_industry_emissions
   - analyze_forecast
   - analyze_maritime
   - OR analyze_table / trader_market_briefing
3. Omit from/to for latest window
4. Present: headline → chart → Statistics → breakdown → EUA implication
5. End: Source: CarbonInsights
```

---

## Executive / stakeholder report

**Triggers:** "write a report", "brief my PM", "executive summary"

```
1. suggest_dataset or confirm table from list_tables
2. executive_briefing({ table })
3. Follow required_output_format in response
4. Structure: Headline → Key findings → Drivers → Implication
5. End: Source: CarbonInsights
```

---

## Historical period analysis

**Triggers:** "June 2020", "compare to last year", "COVID period"

```
1. Confirm table via list_tables
2. analyze_table({ table, from: "YYYY-MM-DD", to: "YYYY-MM-DD" })
   OR compare_periods({ table, period_a_*, period_b_* })
3. Cite date_coverage from tool output
4. State EUA read for that period only — do not imply current unless asked
```

---

## Week-over-week

**Triggers:** "week over week", "last week vs previous week"

```
1. Confirm table has date column
2. compare_recent_weeks({ table })
3. Lead with largest % changes
4. State EUA direction from emission move
5. Include comparison chart
```

---

## Country ranking

**Triggers:** "top emitters", "which country", "rank by emissions"

```
1. suggest_dataset({ topic: "power emissions" }) or user-specified table
2. rank_countries({ table, group_by: "country_code" })
3. Present top 5 with exact figures from breakdown
```

---

## Raw data export

**Triggers:** "give me the raw data", "export CSV", "all rows"

```
1. get_table_structure({ table })    → confirm columns
2. get_table_data({ table, limit, sort, order, from?, to? })
3. Present formatted table — not raw JSON unless requested
```

For analysis questions, still prefer `analyze_table`.

---

## Error handling

| Error | Action |
|-------|--------|
| 401 / MISSING_API_TOKEN | Guide user to MCP config or OAuth login — see setup.md |
| 403 | Table not in API key — call `list_tables`, pick allowed name |
| 429 | Reduce `limit`, paginate, or ask user to wait |
| No accessible tables | User must enable tables in Dashboard → API Keys |
| Unknown table name | Never guess — `list_tables` or `suggest_dataset` |

---

## Analysis output fields (what to cite)

Every `analyze_table` / domain tool response includes:

| Field | Use in user answer |
|-------|-------------------|
| `insights` | Executive summary bullets — lead with these |
| `numeric_summary` | Statistics table — cite mean, trend, change_pct |
| `group_breakdown` | Top countries, ports, segments |
| `date_coverage` | State the actual period analyzed |
| `llm_instructions` | Follow presentation rules in response |
| `eua_bias` (desk) | Bullish/bearish/neutral per dataset |
| `unified_eua_read` (desk) | Composite desk read |

---

## Multi-table desk output structure

Present in this order:

1. **Composite EUA read** — `unified_eua_read.composite_bias` + rationale
2. **Charts** — one per major domain with data
3. **Power** — desk signals for power domain
4. **Industry** — industry/aviation signals
5. **Maritime** — shipping / ETS cost signals
6. **Forecast** — forward outlook signals
7. **Market** — futures/price datasets if present
8. **Source: CarbonInsights**

---

## Morning desk note

**Triggers:** "morning note", "what moved overnight", "desk alerts", "open the desk"

Use MCP prompt: `morning-desk-note`

```
1. desk_alert_scan({ threshold_pct: 10 })
2. multi_table_desk_briefing({})
3. fundamentals_price_read({})
4. Optional: get_chart_series for price + top emission series
5. Follow reference/templates/daily-desk-brief.md
```

---

## Fundamentals vs EUA price

**Triggers:** "fundamentals vs price", "is EUA priced right", "divergence", "price vs emissions"

```
1. fundamentals_price_read({})
2. Lead with divergence flag (aligned / divergent / mixed)
3. Chart: emissions signal + EUA Close from get_chart_series
```

---

## Fuel switch monitor

**Triggers:** "gas vs coal", "fuel switch", "merit order", "power stack"

```
1. analyze_fuel_switch({})
2. Present gas_change_pct vs coal_change_pct
3. EUA intensity implication
```

---

## Year-over-year

**Triggers:** "YoY", "vs last year", "year over year"

```
1. compare_yoy({ table, window_days: 7 })
2. Highlight largest YoY % changes
3. EUA bias from emission direction
```
