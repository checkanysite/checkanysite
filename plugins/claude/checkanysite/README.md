# CheckAnySite

What a website is, with evidence: AI website builder traces, how ready it is for AI tools, popularity from public ranked lists, its technology, trust signals and score, what it is and its domain history. Every request needs a key, free with 300 credits a month: sign in with OAuth, or send a CheckAnySite API key.

This plugin adds CheckAnySite's MCP server and its agent skill to Claude: Claude Code, Cowork and claude.ai. Ask about any public website, and the agent answers with the evidence behind each finding: the line, header or record it rests on, with its source and date. None calls a site safe or a scam.

## Tools

- `check_website`: Everything we know about a website in one call: AI website builder traces, how ready it is for AI tools, popularity, the technology it runs on, trust signals and score, what it is, and its domain history, each finding with its evidence or source (its DNS records ride along in the structured result).
- `detect_ai_builder`: Whether a website shows traces of an AI website builder (such as Lovable, Bolt, v0, Base44 or Replit) or of another site builder, with the evidence line for each.
- `get_ai_readiness`: How easily AI tools (assistants, AI search and agents) can find, read and use a website: a score out of 100 from checks such as its text without scripts, a search listing, a title and description, structured data, a sitemap, llms.txt and files for AI agents (an MCP server card, an API catalog, agent skills), each with its evidence; the level it reaches; and for each gap what to do, with a prompt for an AI coding assistant.
- `get_popularity`: How popular a website is, from public ranked lists (Chrome UX Report, Majestic Million): a band such as "Top 100K" and each list's rank.
- `get_tech_stack`: The technologies a website shows (frameworks, site builders, shop systems, analytics, servers) with the evidence for each, and the network announcing its address.
- `get_dns_records`: A domain's DNS records as we read them over DNS over HTTPS (A, AAAA, CNAME, MX, TXT, NS, CAA, and the AI agents a site names under _agents), whether its answer was validated with DNSSEC, and the network announcing its address.
- `get_trust_signals`: Signals about how established and reachable a website is: contact and company details, policy pages, domain age, HTTPS and security setup, and a score out of 100 for how established it looks.
- `get_domain_history`: A domain's history from public records: when it was registered (domain registry), its first TLS certificate (certificate logs) and when the web archive first captured it.

## What it sends, and where

- **Nothing runs on your machine.** The MCP server runs on our side, at https://checkanysite.com/mcp, over HTTPS.
- **A tool call sends the domain or address you ask about** to that server. CheckAnySite reads the public website, its DNS and public records, and answers. The result is stored and has its own page on https://checkanysite.com, as it would for anyone who checks the site there.
- **You sign in once, with OAuth in your browser,** to a free CheckAnySite account with 300 credits a month. No file here holds a key.
- **The agent skill** tells the agent when to use the tools and how to report what they find. It sends nothing itself.

How we handle the data is in our [privacy policy](https://checkanysite.com/privacy); using the service follows its [terms](https://checkanysite.com/terms). Help and security reports: [contact](https://checkanysite.com/contact).

## License

MIT, for this plugin's files ([the repository](https://github.com/checkanysite/checkanysite)). Using the service follows its [terms](https://checkanysite.com/terms).
