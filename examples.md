# CarbonInsights MCP — Examples

Good vs bad LLM responses when using CarbonInsights MCP.

---

## Full desk briefing

### Good

> **EUA fundamentals: bearish.** CarbonInsights desk aggregation shows 3 of 5 emission datasets trending higher, led by EU power (+17% over the latest window).
>
> ```mermaid
> xychart-beta
>     title "EU Power CO₂ — Daily (CarbonInsights)"
>     x-axis [Jun 1, Jun 5, Jun 10, Jun 15]
>     y-axis "Mt CO₂/day" 0.8 --> 1.3
>     line [0.95, 1.02, 1.08, 1.09]
> ```
>
> **Key findings**
> - Power emissions averaged **1.09 Mt CO₂/day**, trending **+17%**
> - Germany (33%) and Poland (27%) lead country breakdown
> - Industry emissions flat; maritime costs elevated on North Sea routes
>
> **EUA implication:** Rising power and stable industry support **bearish EUA** fundamental pressure across the desk.
>
> *Source: CarbonInsights.*

### Bad

> I don't have access to real-time data. Based on general market knowledge, EUA prices might be around €80. The data could be incomplete so take this with a grain of salt.

**Why bad:** External knowledge, disclaimers, no tool calls, invented price.

---

## Single-table power analysis

### Good

> CarbonInsights shows EU power emissions averaged **1.09 Mt CO₂/day** in the latest window (Jun 1–17), trending **+17%**. Gas emissions rose **+42%**, driving the increase. Germany leads at **33%** of the total.
>
> **EUA read:** Bullish — rising power-sector CO₂ increases allowance demand → price support.
>
> *Source: CarbonInsights.*

### Bad

> Here's the raw JSON from the API: `{"data": [...]}` — you can analyze it yourself. Note that this might not include all countries.

**Why bad:** Raw JSON dump, caveat, no trader framing.

---

## Tool selection

### Good

User: "Give me a full EUA desk report"

→ `multi_table_desk_briefing({})` → present `unified_eua_read` first

### Bad

User: "Give me a full EUA desk report"

→ `trader_market_briefing({ table: "<one table from list_tables>" })` only

**Why bad:** Full-desk questions require multi-table aggregation.

---

## Recency

### Good

User: "What's the current power emissions trend?"

→ `analyze_power_emissions({})` — no `from`/`to` → latest window

Cite `date_coverage` from response: "Latest window: Jun 1–17, 2026"

### Bad

→ `analyze_power_emissions({ from: "2024-01-01", to: "2024-12-31" })` without user asking for 2024

**Why bad:** Defaults to stale historical data when user wants current fundamentals.

---

## Country ranking

### Good

> **Top EU power emitters (CarbonInsights, latest window):**
> 1. Germany — **12.4 Mt CO₂** (33%)
> 2. Poland — **10.1 Mt CO₂** (27%)
> 3. Italy — **4.2 Mt CO₂** (11%)
>
> *Source: CarbonInsights.*

### Bad

> Germany is typically the largest emitter in Europe. Poland also emits a lot of coal power.

**Why bad:** Training knowledge, no exact figures from tools.

---

## Auth failure

### Good

> Your CarbonInsights MCP connection isn't authenticated. In Cursor, add your API key to `mcp.json` under `headers.X-API-Key`, or in Claude use the CarbonInsights connector and sign in via OAuth. Then I can call `verify_api_token` to confirm access.

### Bad

> Please paste your API key here so I can query the data.

**Why bad:** Never ask for API keys in chat when MCP config or OAuth handles auth.

---

## Mermaid chart example (country breakdown)

```mermaid
bar
    title Top EU Power Emitters (CarbonInsights)
    x-axis [Germany, Poland, Italy, France, Spain]
    y-axis "Mt CO₂" 0 --> 15
    bar [12.4, 10.1, 4.2, 3.8, 2.9]
```

Use only numbers returned by `analyze_table` or domain tool breakdown fields.

---

## Session init (skipped)

### Good

User: "What's the EUA desk read?"

→ `get_analysis_rules()` → `list_tables()` → `multi_table_desk_briefing({})` → trader briefing with charts

### Bad

User: "What's the EUA desk read?"

→ `multi_table_desk_briefing({})` only (skipped rules + list_tables)

**Why bad:** Session init not completed; model may not know desk policy or accessible tables.

---

## "Rate the data" — clarify intent

Often "rate the data" means "what does the desk show?" — a market read, not a product score.
Both are legitimate; if it's ambiguous, deliver the market read and offer the other.

### Good (market read)

User: "Rate the CarbonInsights data from the briefing"

→ `get_analysis_rules()` → `list_tables()` → `multi_table_desk_briefing({})` →

> **EUA fundamentals: neutral.** CarbonInsights desk aggregation: power **-11%** (bearish), aviation **-13%** (bearish), aggregate emissions **+6%** (bullish). Maritime voyage costs: latest window **May 26–27** per `date_coverage`.
>
> *Source: CarbonInsights.*

### Also fine (product feedback, if that's what they meant)

> If you want a product view rather than the market read: coverage is strong on power and aviation; the maritime window is short (May 26–27), so treat maritime conclusions as provisional. Want the full EUA desk read too?

Note the market-read numbers are grounded in tool output; any product-quality comment is
clearly separated from them.

---

## Regime indicator signal

### Good

User: "What's the latest regime indicator saying?"

→ `list_tables()` → read `indicator_products` → `get_latest_snapshot({ table })` where `table` comes from catalog →

> **↑ Up** EUA technical signal — CarbonInsights regime indicator (2026-06-24).
>
> **Signal:** ↑ Up | **Confidence:** 67.2% | **Regime:** Renewables-driven (emerald)
>
> Close **€72.45**; renewables-driven regime (ID 1) — strongest historical hit rate bucket.
>
> **EUA implication:** Short-term bullish **price** bias from the model. Cross-check fundamentals separately.
>
> *Source: CarbonInsights.*

### Bad

> The regime model is probably around 60% accurate based on industry standards. Signal might be up but I can't verify.

**Why bad:** Training-memory accuracy, disclaimer, no tool figures.

---

## Signal scoreboard (multi-table desk)

### Good

Uses `eua_bias` from `multi_table_desk_briefing` desk_signals without relabeling:

> **Power daily emissions −3.7%** (red Δ) → **Bearish** EUA (lower allowance demand → price pressure)  
> **Solar generation +19.1%** (green Δ) → **Bearish** EUA (displaces fossil burn)  
> **Fossil gas generation +21.2%** (green Δ) → **Bullish** EUA  
> **Power load +8.6%** (green Δ) → **Bullish** EUA  
> **Aviation −12.9%** (red Δ) → **Bearish** EUA

### Bad

> Power emissions **down 3.7%** — **Bullish** or **Neutral**  
> Solar **up 19%** — **Bullish**  
> Fossil gas **up 21%** — **Bearish**  
> Aviation **down 13%** — **Bullish**

**Why bad:** Inverted price lens. Emissions down = **bearish** EUA price; renewables up = **bearish**; fossil gas up = **bullish**. Do not equate metric +/- color with EUA bias on every row.
