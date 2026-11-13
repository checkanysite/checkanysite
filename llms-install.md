# Installing CheckAnySite

CheckAnySite is a remote MCP server over Streamable HTTP at https://checkanysite.com/mcp. Nothing needs installing or building.

1. Ask the user for a CheckAnySite API key. A free one, with 300 credits a month, comes from https://checkanysite.com/account/keys.
2. Add the server to the MCP settings, with the key in the header:

```json
{
  "mcpServers": {
    "checkanysite": {
      "type": "streamableHttp",
      "url": "https://checkanysite.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

3. Check it works: ask for the tech stack of stripe.com, which calls `get_tech_stack`.
