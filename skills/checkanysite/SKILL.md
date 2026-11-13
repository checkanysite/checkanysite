---
name: checkanysite
description: Find out what a website is, with evidence for every answer. Tells whether it was built with an AI website builder (Lovable, Bolt, v0 and others), how ready it is for AI tools and what to fix, how popular it is, what it runs on, its trust signals, what it does and how old its domain is. Use it when the user asks about a specific website or domain. Needs a CheckAnySite API key in the CHECKANYSITE_API_KEY environment variable.
---

# CheckAnySite

CheckAnySite answers “what is this website?” with evidence. Use it when the user asks about a specific site: whether it was built with an AI website builder, whether AI tools can find, read and use it, how popular or established it is, what it runs on, who is behind it, or how old the domain is.

## Setup

- The user needs an API key, free during launch at https://checkanysite.com/account/keys (300 credits a month; more on request).
- Read it from `CHECKANYSITE_API_KEY`. Never print it, and never put it in a URL.
- If the CheckAnySite MCP server is connected (https://checkanysite.com/mcp), use its tools instead: `check_website`, `detect_ai_builder`, `get_ai_readiness`, `get_popularity`, `get_tech_stack`, `get_dns_records`, `get_trust_signals`, `get_domain_history`.

## Calls

Ask only for the checks the user's question needs: `ai`, `readiness`, `popularity`, `tech`, `dns`, `trust`, `summary` or `history`. Each check costs credits on its own: 1–2 from a stored result, or 1–6 with a new scan. Leave out `checks` to ask for all of them (3 credits stored, 15 with a new scan).

1. Get our stored result, with the checks listed in `?checks=` and separated by commas:

   ```bash
   curl -s "https://api.checkanysite.com/v1/sites/wikipedia.org?checks=ai,dns" -H "Authorization: Bearer $CHECKANYSITE_API_KEY"
   ```

2. If the API returns 404 `no_result`, or the result is too old for the question (check `scannedAt`), start a scan with the same checks:

   ```bash
   curl -s -X POST https://api.checkanysite.com/v1/scans -H "Authorization: Bearer $CHECKANYSITE_API_KEY" \
     -H "Content-Type: application/json" -d '{"domain": "wikipedia.org", "checks": ["ai", "dns"]}'
   ```

3. Read the scan at `links.self` every 3 seconds until `complete` is true; reading a scan is free. The first results arrive within seconds, and slower sources follow.

To verify a fix to a site’s AI readiness, start a scan with `"checks": ["readiness"], "again": true` once the change is live. The check runs again once its last result is 3 minutes old.

For several sites, `POST https://api.checkanysite.com/v1/sites/batch` looks up as many as 50 at once, and `POST https://api.checkanysite.com/v1/scans/batch` scans as many as 10; both take `{"domains": [...]}`. Send an `Idempotency-Key` header with every POST request, and the same one when you retry it, so a retry is never charged twice.

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
- Errors come as `{"error": {"code", "message", "docs"}}`; every code is explained at https://docs.checkanysite.com/errors.
- Watch the credits: prefer stored results. `GET https://api.checkanysite.com/v1/usage` shows what is left.
- A read-only key gets 403 `read_only_key` when it tries to start a scan. Use stored results, or ask the user for a key with full access.
- On 429 `rate_limited`, wait the seconds in `Retry-After`. On `quota_exceeded`, `key_limit_reached` or `scan_limit_reached`, stop and tell the user.

Reference: https://docs.checkanysite.com/llms-full.txt · OpenAPI: https://api.checkanysite.com/v1/openapi.json
