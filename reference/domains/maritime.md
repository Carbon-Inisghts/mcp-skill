# Maritime Domain — EU ETS

## Datasets (discover via `list_tables`)

- Voyage-level emissions + EU ETS trip costs
- Daily distances + emissions by vessel type
- Sample trip cost datasets

Use `analyze_maritime({})` to auto-select from accessible maritime tables.

## Tools

| Question | Tool |
|----------|------|
| Maritime analysis | `analyze_maritime` |
| Port ranking | `analyze_maritime` with port `group_by` |
| Alert on trip emissions spike | `desk_alert_scan` |

## EUA linkage

| Signal | EUA read |
|--------|----------|
| Voyage emissions ↑ | Bearish EUA |
| EU ETS distance / coverage ↑ | Bearish EUA |
| Trip costs ↑ | Higher compliance demand → bearish |

## Presentation

Rank top departure ports. Cite `date_coverage` from tool output for the window analyzed.
