# CarbonInsights UI Response Palette

Match the CarbonInsights webapp dashboard when formatting trader-facing LLM answers.
Sourced from `webapp/app/globals.css` and `webapp/lib/colors.ts`.

## Brand tokens

| Token | Light | Dark | Use |
|-------|-------|------|-----|
| `--ci-primary` | `#15803d` | `#22c55e` | Brand green, power sector, primary actions |
| `--ci-secondary` | `#76f549` | `#86efac` | Highlights |
| `--ci-tertiary` | `#1480cf` | `#38bdf8` | Info, links |
| `--ci-accent` | `#d97706` | `#f59e0b` | Aviation, warnings, probability bars |
| `--ci-dark` | `#2c3e50` | `#94a3b8` | Industry sector |
| `--ci-muted` | `#64748b` | `#94a3b8` | Secondary labels |
| `--ci-red` | `#dc2626` | `#ef4444` | Bearish / Down |
| `--ci-green` | `#16a34a` | `#22c55e` | Bullish / Up |

## Directional signals

| Signal | Label | Color class (webapp) |
|--------|-------|----------------------|
| Up / bullish | **↑ Up** or **BULLISH** | `text-emerald-600` / `dark:text-emerald-400` |
| Down / bearish | **↓ Down** or **BEARISH** | `text-red-600` / `dark:text-red-400` |
| Neutral | **→ Neutral** | `text-amber-600` or muted |

## Sector colors (`SECTOR_COLORS`)

| Sector | CSS var | Hex (light) |
|--------|---------|-------------|
| Power | `--ci-sector-power` | `#15803d` |
| Industry | `--ci-sector-industry` | `#2c3e50` |
| Aviation | `--ci-sector-aviation` | `#d97706` |
| Maritime | `--ci-sector-maritime` | `#0d9488` |

## Chart series (use in order)

| Series | Hex | Token |
|--------|-----|-------|
| 1 | `#3b82f6` | chart-1 |
| 2 | `#10b981` | chart-2 |
| 3 | `#f59e0b` | chart-3 |
| 4 | `#ef4444` | chart-4 |
| 5 | `#8b5cf6` | chart-5 |

## Regime indicator colors (regime dashboard)

| Regime | Chart token | Color |
|--------|-------------|-------|
| Trending | chart-1 | Blue `#3b82f6` |
| Renewable-driven | chart-2 | Emerald `#10b981` |
| Fossil-driven | chart-4 | Red `#ef4444` |
| Mean Reverting | chart-3 | Amber `#f59e0b` |
| Neutral | chart-5 | Purple `#8b5cf6` |

## Delta semantics (ETS scenario desk)

| Direction | Color | Meaning |
|-----------|-------|---------|
| Tightening | `--ci-delta-tightening` (red) | Supply tightening |
| Loosening | `--ci-delta-loosening` (green) | Supply loosening |

## Formatting rules

- **Prices:** `€XX.XX` (two decimals)
- **Emissions:** cite units from tool output (t CO₂, Mt CO₂)
- **Probability:** `XX.X%` from `predicted_probability × 100`
- **Sentiment score:** 0–30 strong bearish, 46–54 neutral, 70–100 strong bullish
- **Layout:** headline → signal badge → 1–3 charts → key readings → EUA implication → *Source: CarbonInsights.*

## MCP resource

Server injects this palette at `carboninsights://docs/ui-palette`.
