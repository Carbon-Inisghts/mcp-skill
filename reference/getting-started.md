# Getting Started — CarbonInsights MCP

## 5-minute setup

### 1. Get your API key
1. Sign in at [carboninsight.com](https://carboninsight.com)
2. Dashboard → **API Keys** → generate key
3. Enable the tables you need (power, industry, maritime, market, etc.)

### 2. Connect your client

**Cursor (local MCP server)**
```json
{
  "mcpServers": {
    "carboninsights": {
      "url": "http://localhost:3100/mcp",
      "headers": {
        "X-API-Key": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

**Claude / ChatGPT** — use the CarbonInsights connector URL and sign in via OAuth.

**Local stdio** — set `CARBONINSIGHT_API_TOKEN` in MCP env.

### 3. Verify access
```
verify_api_token()
list_tables()
```

### 4. Run your first briefing
```
multi_table_desk_briefing({})
```

### 5. Morning desk workflow
```
desk_alert_scan({ threshold_pct: 10 })
fundamentals_price_read({})
```

## What you get

- **25 MCP tools** — analysis, desk aggregation, market, fuel switch, alerts, chart series
- **19 MCP prompts** — morning desk, EUA market, fuel switch, aviation, full desk
- **Senior EUA trader persona** — bullish/bearish/neutral reads with charts

## Next steps

- [datasets.md](datasets.md) — table catalog
- [tools.md](tools.md) — full tool reference
- [workflows.md](workflows.md) — step-by-step playbooks
- [templates/daily-desk-brief.md](templates/daily-desk-brief.md) — report template
