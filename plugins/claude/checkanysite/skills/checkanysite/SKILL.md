---
name: checkanysite
description: Find out what a website is, with evidence for every answer. Tells whether it was built with an AI website builder (Lovable, Bolt, v0 and others), how ready it is for AI tools and what to fix, how popular it is, what it runs on, its trust signals, what it does and how old its domain is. Use it when the user asks about a specific website or domain. Uses the CheckAnySite MCP server that comes with it, which signs the user in.
---

# CheckAnySite

CheckAnySite answers “what is this website?” with evidence. Use it when the user asks about a specific site: whether it was built with an AI website builder, whether AI tools can find, read and use it, how popular or established it is, what it runs on, who is behind it, or how old the domain is.

## Tools

This plugin's MCP server, `checkanysite`, runs at https://checkanysite.com/mcp. It signs the user in with OAuth the first time a tool is used; nothing else needs setting up. Call the tool that answers the question, with the domain:

- `check_website`: Everything we know about a website in one call: AI website builder traces, how ready it is for AI tools, popularity, the technology it runs on, trust signals and score, what it is, and its domain history, each finding with its evidence or source (its DNS records ride along in the structured result).
- `detect_ai_builder`: Whether a website shows traces of an AI website builder (such as Lovable, Bolt, v0, Base44 or Replit) or of another site builder, with the evidence line for each.
- `get_ai_readiness`: How easily AI tools (assistants, AI search and agents) can find, read and use a website: a score out of 100 from checks such as its text without scripts, a search listing, a title and description, structured data, a sitemap, llms.txt and files for AI agents (an MCP server card, an API catalog, agent skills), each with its evidence; the level it reaches; and for each gap what to do, with a prompt for an AI coding assistant.
- `get_popularity`: How popular a website is, from public ranked lists (Chrome UX Report, Majestic Million): a band such as "Top 100K" and each list's rank.
- `get_tech_stack`: The technologies a website shows (frameworks, site builders, shop systems, analytics, servers) with the evidence for each, and the network announcing its address.
- `get_dns_records`: A domain's DNS records as we read them over DNS over HTTPS (A, AAAA, CNAME, MX, TXT, NS, CAA, and the AI agents a site names under _agents), whether its answer was validated with DNSSEC, and the network announcing its address.
- `get_trust_signals`: Signals about how established and reachable a website is: contact and company details, policy pages, domain age, HTTPS and security setup, and a score out of 100 for how established it looks.
- `get_domain_history`: A domain's history from public records: when it was registered (domain registry), its first TLS certificate (certificate logs) and when the web archive first captured it.

Each tool answers from our newest stored result by default; with `source: "scan"` it scans the site now, which costs more credits. A tool for one question costs fewer credits than `check_website`. To verify a fix to a site’s AI readiness, call `get_ai_readiness` with `source: "scan"` once the change is live.

## Reading the result

- `ai.level`: `high` (an AI builder’s own trace), `medium` (several weaker traces together) or `none`; `ai.builders[].evidence` holds the exact line.
- `readiness`: how easily AI tools can find, read and use the site, with a `score` out of 100 and the `level` it reaches. Each item of `checks[]` has its evidence and, when it isn’t met, a `fix` with a prompt for an AI coding assistant (`fixPrompt` combines them). `crawlers[]` lists what the site’s robots.txt allows each AI crawler to do; that is the site’s choice and isn’t scored.
- `popularity.band`: a band such as “Top 100K” from public ranked lists; never a visit count.
- `tech.technologies[]`: what the site runs on, each with its evidence.
- `dns.records[]`: the domain’s DNS records (A, AAAA, CNAME, MX, TXT, NS, CAA), with `dnssec` and the `network` announcing its address.
- `trust.checks[]` and `score`: signals of how established the site looks (contact details, policies, domain age, HTTPS). The score never says whether a site is honest.
- `summary`: what the site says it is, its kind, and who is behind it, by source.
- `history`: registration date, first certificate and first web archive capture.
- `limited`: we couldn’t read the page itself (bot protection, robots.txt or a sign-in wall), so the result comes from outside records.

## Rules

- Report what was found, with its evidence or source, and link to `resultUrl` for the full result.
- Present findings as signals, not verdicts: never call a site safe, legitimate, a scam or fake.
- Check `scannedAt`: a stored result can be old. Scan again when the question is about the site as it is now.
- When a tool says the credits are used up or a limit is reached, stop and tell the user.

Reference: https://docs.checkanysite.com/mcp
