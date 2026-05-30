# OpenCapital MCP Server

**Every US public company, sourced from SEC filings — now available to your AI assistant.**

OpenCapital is a hosted [Model Context Protocol](https://modelcontextprotocol.io) (MCP) server that gives Claude, ChatGPT, Cursor, Codex, and any other MCP-capable client **read-only** access to what every US public company actually reports — fundamentals, segment breakdowns, peer comparisons, and earnings for thousands of US-listed equities (common shares and ADRs), all derived directly from SEC filings.

You don't run anything. The server is hosted on OpenCapital's infrastructure. You add one URL to your client, sign in once, and start asking.

```
https://api.opencapital.sh/mcp
```

- **Transport:** Streamable HTTP (remote MCP server)
- **Auth:** OAuth 2.0 — sign in with Google, grant read-only access
- **Free tier:** 100 queries/day, no credit card. Paid plans remove the cap.
- **Data:** Fundamentals, segments, and earnings derived from US SEC filings (10-K, 10-Q, 8-K), read live

> The data is free, the workflow is paid. Every metric, segment, quarter, and filing reference is free to query. [OpenCapital](https://opencapital.sh) is a small, independent project — not affiliated with the SEC.

---

## Quick connect

Pick your client below, or see the full step-by-step guides at **[opencapital.sh/connect-ai](https://opencapital.sh/connect-ai)**.

### Claude (claude.ai / Claude Desktop)

1. **Customize** → **Connectors** → **Add custom connector**
2. Name it `OpenCapital`, paste `https://api.opencapital.sh/mcp`
3. Click **Connect** and authorize read-only access

Full guide: [opencapital.sh/connect-ai/claude](https://opencapital.sh/connect-ai/claude)

### Claude Code

```bash
claude mcp add --transport http opencapital https://api.opencapital.sh/mcp
```

Add `--scope user` to make it available in every project. Then run `/mcp` inside a session, select **opencapital**, and choose **Authenticate**.

Full guide: [opencapital.sh/connect-ai/claude-code](https://opencapital.sh/connect-ai/claude-code)

### ChatGPT (Plus / Team / Enterprise)

1. **Settings** → **Apps** → **Advanced settings** → enable **Developer mode**
2. **Create app**, name it `OpenCapital`, paste the URL, select **OAuth**
3. Authorize read-only access

Full guide: [opencapital.sh/connect-ai/chatgpt](https://opencapital.sh/connect-ai/chatgpt)

### Cursor

Add to `~/.cursor/mcp.json` (global) or `.cursor/mcp.json` (project):

```json
{
  "mcpServers": {
    "opencapital": {
      "url": "https://api.opencapital.sh/mcp"
    }
  }
}
```

Then enable the server under **Cursor Settings → Tools & MCP → Connect**.

Full guide: [opencapital.sh/connect-ai/cursor](https://opencapital.sh/connect-ai/cursor)

### Codex / Codex CLI

```bash
codex mcp add opencapital --url https://api.opencapital.sh/mcp
codex mcp login opencapital
```

Or add to `~/.codex/config.toml`:

```toml
[mcp_servers.opencapital]
url = "https://api.opencapital.sh/mcp"
```

Full guides: [codex](https://opencapital.sh/connect-ai/codex) · [codex-cli](https://opencapital.sh/connect-ai/codex-cli)

### Any other MCP client

Add a **remote / custom MCP server** over the **Streamable HTTP** transport, pointing at `https://api.opencapital.sh/mcp`. Most clients also accept the `mcpServers` JSON shape shown in the Cursor section above. The first call opens your browser to sign in and approve read-only access.

Full guide: [opencapital.sh/connect-ai/other](https://opencapital.sh/connect-ai/other)

---

## What you can ask

The server ships with 13 read-only tools. You rarely call them by name — just ask in natural language and your client picks the right one.

| Tool | What it does |
|------|--------------|
| `stock_screener` | Find and filter companies (sector, market cap, P/E, growth, FCF…). One row per company. |
| `stock_screener_filter_values` | List valid values for a stock filter field (e.g. count of stocks per sector). |
| `metric_screener` | Search financial metrics across companies. One row per (company × metric), with latest value, YoY/QoQ, and TTM change. |
| `metric_screener_filter_values` | List valid values for a metric filter field. |
| `metric_detail` | Definition, plain-language meaning, signal interpretation, parent/standard metric, and similar metrics across peers. |
| `metric_time_series` | Full quarterly / annual / TTM history for one or more metrics on a single ticker. |
| `peer_time_series` | One metric across up to 10 tickers — head-to-head peer comparisons. |
| `segment_time_series` | Segment disaggregation (product, business, geography) for a line item, with history per segment. |
| `business_overview` | What a company does, from its latest 10-K Item 1: segments, value chain, partnerships, named competitors. |
| `business_competitors` | Ranked peer list — competitors named in filings, reverse mentions, and embedding-similar businesses. |
| `portfolio_holdings` | Your linked brokerage holdings, aggregated by ticker with weights and P&L. *(requires sign-in + linked account)* |
| `get_watchlist` | Your watchlist with company metadata and nearest earnings event. *(requires sign-in)* |
| `update_watchlist` | Add or remove tickers from your watchlist. *(requires sign-in)* |

### Example prompts

- *"What's Uber's Mobility take rate over the last 8 quarters?"*
- *"How does Airbnb's ADR compare across regions?"*
- *"Show me DoorDash Marketplace GOV every quarter since IPO."*
- *"Compare cloud revenue across AWS, Azure, GCP, and Oracle."*
- *"Find me 10 large-caps growing revenue over 20% with positive free cash flow and a P/E under 30."*
- *"Before Nvidia reports, summarize what their suppliers, hyperscaler customers, and competitors said in their last filings."*

More in [`examples/prompts.md`](examples/prompts.md).

---

## Read-only by design

The OpenCapital MCP server only exposes read-only stock research data — fundamentals, segments, and earnings derived from public SEC filings. Your assistant **cannot place trades or modify any account state.** The watchlist tools are the only write surface, and they only edit your own OpenCapital watchlist.

## Privacy & terms

OAuth grants your AI client read-only access to OpenCapital's public stock research index (and, if you choose, your own watchlist and linked-brokerage holdings). See the [Terms of Service](https://opencapital.sh/terms) and [Privacy Policy](https://opencapital.sh/privacy).

## License

The configuration snippets and documentation in this repository are [MIT-licensed](LICENSE).

The OpenCapital MCP service they connect to is a hosted service governed by its [Terms of Service](https://opencapital.sh/terms) — your use of the service, including the free tier, is subject to those terms, not this license. This repository does not contain the server's source code.

## Links

- Website — [opencapital.sh](https://opencapital.sh)
- Connect guides — [opencapital.sh/connect-ai](https://opencapital.sh/connect-ai)
- Model Context Protocol — [modelcontextprotocol.io](https://modelcontextprotocol.io)
