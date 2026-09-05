---
name: regulatory-check
description: Check what US federal or state regulations changed recently for a given industry, agency, or topic, with citations. Use when the user asks about new rules, compliance changes, regulatory updates, or grant opportunities in a jurisdiction.
---

# Regulatory check

Use the Bizmoon MCP tools in this order:

1. `list_jurisdictions` once per session to learn coverage and freshness. Tell the user the
   latest publication date for the jurisdiction they care about.
2. `search_regulatory_changes` with `jurisdiction` (two-letter state or `US_FED`), a
   `keyword` for the topic, and `from` for the window the user asked about. Use `agency`
   when they name one.
3. For anything you will summarize, call `get_regulatory_change` on the id and quote the
   `effectiveDate` and `url`.
4. For grants or incentives, use `search_funding_programs` instead.

Rules:
- Always cite the `url` for every change you mention. Never state an effective date
  without one from the tool.
- If a result has `lookbackClampedTo`, tell the user the free tier only covers the last
  90 days and that an API key at https://bizmoon.ai/mcp unlocks full history.
- If you get `rate_limited`, wait `retryAfterSeconds` or tell the user the daily free
  quota is used up.
- Present results as a dated list: date, jurisdiction, agency, one-line summary, link.
