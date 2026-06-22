# CarbonInsights MCP — Client Setup

How to authenticate the MCP server per client. The LLM should guide users here on auth failures — never ask them to paste API keys into chat when OAuth is available.

---

## Authentication options

| Client | Method | API key in chat? |
|--------|--------|------------------|
| **Claude (web)** | Supabase OAuth login | No |
| **ChatGPT** | OAuth connector | No |
| **Cursor (remote)** | `X-API-Key` in mcp.json headers | No |
| **Cursor (local stdio)** | `CARBONINSIGHT_API_TOKEN` in env | No |

The CarbonInsights **data API** uses API keys internally. With OAuth, the MCP server looks up the user's key after sign-in — the LLM never sees it.

---

## Get API token (dashboard)

1. Sign in at [carboninsight.com](https://carboninsight.com)
2. Go to **Dashboard → API Keys**
3. Select tables and click **Generate API Key**

OAuth users must have at least one API key stored for their account (linked by Supabase user id).

---

## Claude / ChatGPT (OAuth) — recommended

### Server requirements

Deploy MCP server with:

```
SUPABASE_URL=https://your-project.supabase.co
MCP_PUBLIC_URL=https://YOUR-SERVICE.onrender.com
SUPABASE_SERVICE_ROLE_KEY=your_service_role_key
```

### Add connector

1. **Settings → Connectors → Add custom connector**
2. **Name:** carboninsights
3. **Remote MCP server URL:** `https://YOUR-SERVICE.onrender.com/mcp`
4. **OAuth Client ID / Secret:** leave empty if Dynamic Client Registration enabled
5. Save → browser login with CarbonInsights account
6. Call `verify_api_token` or `list_tables` — no API key in chat

**Do not** paste the CarbonInsights API key into OAuth Client Secret.

---

## Cursor (hosted / remote)

`mcp.json`:

```json
{
  "mcpServers": {
    "carboninsights": {
      "url": "https://YOUR-SERVICE.onrender.com/mcp",
      "headers": {
        "X-API-Key": "${env:CARBONINSIGHT_API_TOKEN}"
      }
    }
  }
}
```

---

## Cursor (local stdio)

```json
{
  "mcpServers": {
    "carboninsights": {
      "command": "node",
      "args": ["/path/to/mcp_server/index.js"],
      "env": {
        "CARBONINSIGHT_API_TOKEN": "your_token_here",
        "CARBONINSIGHT_API_BASE_URL": "https://api.carboninsight.com/api"
      }
    }
  }
}
```

---

## Verify setup

| Check | How |
|-------|-----|
| OAuth metadata | `GET /.well-known/oauth-protected-resource` |
| Health | `GET /health` → `"oauth": true` when configured |
| MCP tools | Call `verify_api_token` or `list_tables` |

---

## Inspector testing (local)

```powershell
$env:CARBONINSIGHT_API_TOKEN="your_token"
npm run inspector
```

Use transport = **STDIO** in Inspector for local testing.

---

## LLM behavior on auth errors

| Situation | Tell user |
|-----------|-----------|
| 401 | Update API token in MCP config or re-authenticate via OAuth |
| No tables | Enable tables in Dashboard → API Keys, then retry `list_tables` |
| 403 on table | Use only table names from `list_tables` output |

Never log, repeat, or display the user's API token in chat.
