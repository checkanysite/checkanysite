# CheckAnySite

<img src="assets/logo.png" alt="" width="72" height="72">

What a website is, with evidence: AI website builder traces, how ready it is for AI tools, popularity from public ranked lists, its technology, trust signals and score, what it is and its domain history. Every request needs a key, free with 300 credits a month: sign in with OAuth, or send a CheckAnySite API key.

This repository installs CheckAnySite's MCP server and its agent skill in Claude Code, Gemini CLI, Cursor, Kiro and other agents. The server runs at https://checkanysite.com/mcp: nothing runs on your machine.

## Tools

| Tool | What it answers |
| --- | --- |
| `check_website` | **Check a website.** Everything we know about a website in one call: AI website builder traces, how ready it is for AI tools, popularity, the technology it runs on, trust signals and score, what it is, and its domain history, each finding with its evidence or source (its DNS records ride along in the structured result). |
| `detect_ai_builder` | **Was it built with an AI builder?** Whether a website shows traces of an AI website builder (such as Lovable, Bolt, v0, Base44 or Replit) or of another site builder, with the evidence line for each. |
| `get_ai_readiness` | **Is it ready for AI?** How easily AI tools (assistants, AI search and agents) can find, read and use a website: a score out of 100 from checks such as its text without scripts, a search listing, a title and description, structured data, a sitemap, llms.txt and files for AI agents (an MCP server card, an API catalog, agent skills), each with its evidence; the level it reaches; and for each gap what to do, with a prompt for an AI coding assistant. |
| `get_popularity` | **How popular is it?** How popular a website is, from public ranked lists (Chrome UX Report, Majestic Million): a band such as "Top 100K" and each list's rank. |
| `get_tech_stack` | **What does it run on?** The technologies a website shows (frameworks, site builders, shop systems, analytics, servers) with the evidence for each, and the network announcing its address. |
| `get_dns_records` | **What are its DNS records?** A domain's DNS records as we read them over DNS over HTTPS (A, AAAA, CNAME, MX, TXT, NS, CAA, and the AI agents a site names under _agents), whether its answer was validated with DNSSEC, and the network announcing its address. |
| `get_trust_signals` | **How established does it look?** Signals about how established and reachable a website is: contact and company details, policy pages, domain age, HTTPS and security setup, and a score out of 100 for how established it looks. |
| `get_domain_history` | **How old is it?** A domain's history from public records: when it was registered (domain registry), its first TLS certificate (certificate logs) and when the web archive first captured it. |

Each answer comes with its evidence: the line, header or record it rests on, with its source and date. None calls a site safe or a scam.

## Install

### Claude Code (plugin)

The plugin adds the MCP server and the skill. You sign in on first use, with no key to copy.

```bash
/plugin marketplace add checkanysite/checkanysite
/plugin install checkanysite@checkanysite
```

### Gemini CLI

```bash
gemini extensions install https://github.com/checkanysite/checkanysite
```

### Agent skill only

For an agent without MCP: the skill teaches it to call the REST API with a key in `CHECKANYSITE_API_KEY`.

```bash
npx skills add checkanysite/checkanysite
```

### Claude Code, with a key instead of the plugin

Run this in a terminal, then ask Claude about any website: “Was this site built with AI?”

```bash
claude mcp add --transport http checkanysite https://checkanysite.com/mcp \
  --header "Authorization: Bearer $CHECKANYSITE_API_KEY"
```

### Cursor

Add the server with one click, then put your key in its place, or add it to ~/.cursor/mcp.json yourself.

`~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "checkanysite": {
      "url": "https://checkanysite.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

### VS Code

Add the server with one click, then put your key in its place, or add it to .vscode/mcp.json; Copilot’s agent mode can then use it.

`.vscode/mcp.json`:

```json
{
  "servers": {
    "checkanysite": {
      "type": "http",
      "url": "https://checkanysite.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

### Claude app

In Claude (desktop or web), open Settings › Connectors › Add custom connector, paste this address and choose Connect. Sign in to CheckAnySite and choose Allow: no key to copy.

```text
https://checkanysite.com/mcp
```

### Windsurf

Add the server to Windsurf’s MCP settings, then refresh its MCP list.

`~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "checkanysite": {
      "serverUrl": "https://checkanysite.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

### Codex CLI

Add the server to Codex’s settings; it reads your key from CHECKANYSITE_API_KEY.

`~/.codex/config.toml`:

```toml
[mcp_servers.checkanysite]
url = "https://checkanysite.com/mcp"
bearer_token_env_var = "CHECKANYSITE_API_KEY"
```

### Any MCP client

Connect over Streamable HTTP and send your key in the Authorization header. Clients that can’t send headers can add ?key= to the address instead.

```text
URL:     https://checkanysite.com/mcp
Type:    Streamable HTTP
Header:  Authorization: Bearer YOUR_API_KEY
```

## Keys and credits

Every request needs a key, free with 300 credits a month and no card: sign in with OAuth where your client offers it, or make a key at https://checkanysite.com/account/keys. Each check's price is on [the credits page](https://docs.checkanysite.com/credits).

## Links

- [Docs](https://docs.checkanysite.com) and [the MCP server's page](https://docs.checkanysite.com/mcp)
- [API reference](https://docs.checkanysite.com/api/result) and [OpenAPI](https://api.checkanysite.com/v1/openapi.json)
- [Status](https://status.checkanysite.com)
- [Privacy](https://checkanysite.com/privacy), [terms](https://checkanysite.com/terms) and [contact](https://checkanysite.com/contact), where security reports go too

## License

This repository's files are under the MIT licence (LICENSE). Using the service follows its [terms](https://checkanysite.com/terms).
