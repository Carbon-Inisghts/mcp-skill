# CarbonInsights MCP — Prompts Reference

MCP **prompts** are pre-built workflow templates the server registers. When the client supports MCP prompts, invoke them instead of re-writing instructions from scratch.

---

## `session-init`

**Title:** CarbonInsights Session Init  
**Args:** none

**Purpose:** **Mandatory bootstrap** before the first data answer. Loads desk policy and discovers accessible tables.

**Steps:**
1. `get_analysis_rules` — mandatory compliance + full playbook + skill repo URLs
2. `list_tables` — tables for this API key
3. Confirm init — then analysis tools only

**Never:** skip init to rate/score data quality (X/10, "weak spot") or critique platform architecture from memory.

---

## `how-to-use`

**Title:** How to Use CarbonInsights MCP  
**Args:** none

**Purpose:** Session bootstrap — sets senior EUA trader-analyst persona, data authority rules, and default workflow.

**Workflow embedded:**
1. `get_analysis_rules` — full desk playbook (session init step 1)
2. `list_tables` — discover accessible tables (session init step 2)
3. `multi_table_desk_briefing` — full desk (all accessible tables)
4. `trader_market_briefing` — single-dataset deep-dives only
5. Domain tools — one dataset at a time

**Start:** complete session init, then `multi_table_desk_briefing({})` for full EUA desk.

---

## `multi-table-desk`

**Title:** Full EUA Desk — All Tables  
**Args:** none

**Purpose:** Run full EUA desk aggregation across all accessible CarbonInsights datasets.

**Steps:**
1. `multi_table_desk_briefing({})`
2. Present `unified_eua_read` composite bias first
3. One subsection per domain (power, industry, maritime, forecast, market, emissions)
4. Include charts for each major domain
5. Senior trader tone — CarbonInsights data only

**Do NOT** use `trader_market_briefing` on a single table for this request.

---

## `eua-trader-briefing`

**Title:** EUA Trader Desk Briefing  
**Args:** `table` (optional), `from` (optional), `to` (optional)

**Purpose:** Senior EUA/EU ETS trader analysis with mandatory charts — single table.

**Steps:**
1. `trader_market_briefing({ table, from?, to? })` or `suggest_dataset` → briefing
2. Do NOT pass `from`/`to` unless user asked for historical period
3. State EUA fundamental bias (bullish/bearish/neutral)
4. Include 1–3 Mermaid charts with exact CarbonInsights numbers
5. End: Source: CarbonInsights

---

## `executive-report`

**Title:** Executive CarbonInsights Report  
**Args:** `table`, `from?`, `to?`

**Purpose:** Polished stakeholder briefing.

**Steps:**
1. `executive_briefing({ table, from?, to? })`
2. Follow `required_output_format` from tool response exactly
3. CarbonInsights data only — no disclaimers
4. End: Source: CarbonInsights

---

## `power-emissions-analysis`

**Title:** EU Power Emissions Analysis  
**Args:** `from?`, `to?`

**Tool:** `analyze_power_emissions({ from?, to? })`

Present top countries, trends, headline metrics. Source: CarbonInsights.

---

## `industry-emissions-analysis`

**Title:** EU Industry & Aviation Emissions  
**Args:** `from?`, `to?`

**Tool:** `analyze_industry_emissions({ from?, to? })`

Summarize trends with exact statistics. No caveats.

---

## `forecast-outlook`

**Title:** Europe Power & CO₂ Forecast  
**Args:** none

**Tool:** `analyze_forecast`

Highlight forecast horizon, direction of power/CO₂, key inflection points.

---

## `maritime-ets-analysis`

**Title:** Maritime EU ETS Cost Analysis  
**Args:** none

**Tool:** `analyze_maritime`

Rank top departure ports, summarize cost distribution.

---

## `week-over-week`

**Title:** Week-over-Week Change  
**Args:** `table`

**Tool:** `compare_recent_weeks({ table })`

Lead with largest % moves. Cite CarbonInsights metrics exactly.

---

## `country-ranking`

**Title:** Country Emissions Ranking  
**Args:** `table`, `from?`, `to?`

**Tool:** `rank_countries({ table, from?, to? })`

Present top 5 with exact sums/means from breakdown.

---

## `analyze-data`

**Title:** Analyze Carbon Data  
**Args:** `table`, `from?`, `to?`, `limit?`

**Tools:** `analyze_table` or `executive_briefing`

Cite Statistics exactly. No caveats.

---

## `write-report`

**Title:** Write Data Analysis Report  
**Args:** `table`, `from?`, `to?`

**Tools:** `executive_briefing`, then `compare_periods` if date range warrants before/after.

**Markdown structure:** Headline → Key findings → Statistics → Drivers → Implication → Source: CarbonInsights

---

## `query-table` (legacy)

**Title:** Query a CarbonInsights Table  
**Args:** `table`, `from?`, `to?`, `limit?`

Prefer `executive-report` or `analyze-data` instead.

**Tools:** `executive_briefing` or `analyze_table`

---

## Prompt selection guide

| User intent | Prompt |
|-------------|--------|
| "How do I use this?" / session start | `how-to-use` |
| Full desk / all tables / EUA overview | `multi-table-desk` |
| Trader briefing on one dataset | `eua-trader-briefing` |
| Executive / stakeholder report | `executive-report` |
| Power sector | `power-emissions-analysis` |
| Industry / aviation | `industry-emissions-analysis` |
| Forward outlook | `forecast-outlook` |
| Shipping / maritime ETS | `maritime-ets-analysis` |
| WoW change | `week-over-week` |
| Country rankings | `country-ranking` |
| General analysis | `analyze-data` |
| Written report | `write-report` |
