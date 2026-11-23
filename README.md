<p align="center">
  <img src="icons/saferate-512.png" width="96" height="96" alt="Safe Rate">
</p>

# Safe Rate MCP server

A hosted [Model Context Protocol](https://modelcontextprotocol.io) server for US
mortgage rate estimates, lender research from public federal HMDA filings, local
housing-market and hazard context, and U.S. Treasury market data.

Rate estimates never ask for a name, email address or phone number.

| | |
|---|---|
| Endpoint | `https://mcp.saferate.com/mcp` |
| Transport | Streamable HTTP |
| Sign-in | Not needed for 17 of the 22 tools (see [Signed-in tools](#signed-in-tools)) |
| Registry | [`com.saferate/saferate`](https://registry.modelcontextprotocol.io/v0/servers?search=com.saferate/saferate) |
| Server card | <https://mcp.saferate.com/.well-known/mcp/server-card.json> |
| Website | <https://saferate.com> |

This repository holds the server's public description: this README, its
[`server.json`](server.json) registry entry, icons and example setups. The server
itself runs on Safe Rate's infrastructure, and its source code is not published.

## Connect

**Claude** (claude.ai and the desktop app): Settings → Connectors → Add custom
connector, URL `https://mcp.saferate.com/mcp`.

**Claude Code**

```sh
claude mcp add --transport http saferate https://mcp.saferate.com/mcp
```

**ChatGPT**: search for Safe Rate in the app directory.

**Any other client** that supports remote Streamable HTTP servers: see
[`examples/`](examples).

## Tools

### Mortgage and lenders

| Tool | What it does |
|---|---|
| `get_quote_estimate` | Mortgage rate estimates for a US location and scenario, from wholesale rate sheets. |
| `track_quote_estimate` | Check an earlier estimate by its estimate ID. Saves and sends nothing. |
| `find_lenders_in_market` | Lenders ranked for a metro area or state, by loan type or institution type. |
| `research_lender` | A lender's origination volume, approval and pull-through rates, product mix and footprint, by name or NMLS ID. |
| `get_market_context` | Median home value and rent, recent price change and mortgage-rate history for a location. |
| `assess_property_context` | FEMA National Risk Index, flood-zone and other hazard exposure that affects insurance. |
| `search`, `fetch` | Search and read Safe Rate's published pages (rate indexes, lender profiles, rankings). |

### U.S. Treasury

| Tool | What it does |
|---|---|
| `get_treasury_curve` | The Treasury yield curve on a date. |
| `get_treasury_rate_history` | History of Treasury yields by tenor. |
| `list_treasury_securities` | Securities outstanding on a date, including which is on-the-run for each tenor. |
| `get_treasury_security` | One security by CUSIP: terms, price history, duration, convexity, DV01, key-rate durations. |
| `price_treasury_security` | Convert between price and yield for a bill, note or bond. |
| `value_savings_bond` | Value a U.S. savings bond. |
| `get_savings_bond_rates` | Current and historical savings bond rates. |
| `get_treasury_index` | Safe Rate's Treasury total-return indices. |
| `get_treasury_debt` | The federal debt statement. |

All 17 tools above are read-only and need no account.

### Signed-in tools

Five tools act on a shopper's own Safe Rate Universal Application and ask the
shopper to sign in with Safe Rate (OAuth) when called:

| Tool | Scope |
|---|---|
| `get_my_application` | read |
| `get_my_quotes` | read |
| `get_share_link` | read |
| `start_my_application` | write |
| `update_my_application` | write |

Sharing an application with a lender and entering a Social Security number always
take the shopper's own click on saferate.com. No tool does either; `get_share_link`
only returns the page where the shopper does it.

## Try it

- What would a $500k place in 60607 cost me monthly with 20% down?
- Who are the top VA lenders in Austin?
- Do I need flood insurance in 33139?
- What is the current 10-year Treasury yielding, and how has it moved this year?

More in [`examples/prompts.md`](examples/prompts.md).

## What the numbers are, and are not

- Rate estimates are non-binding and are not offers to lend. A quote comes only
  from a lender the borrower asks for one. Every estimate carries its as-of date.
- Lender rankings come from public federal HMDA filings. Placement cannot be
  bought.
- Safe Rate Mortgage (NMLS #1590949) is affiliated with Safe Rate and is
  disclosed wherever it appears. It is licensed to lend in Illinois only. Equal
  Housing Lender.
- Treasury figures are published end-of-day federal data, not live prices and not
  investment advice. The total-return indices are built by Safe Rate and are not
  official U.S. Treasury statistics.
- Nothing the server returns is financial advice.

## Links

- Privacy: <https://saferate.com/privacy-policy>
- Terms: <https://saferate.com/terms-of-use>
- Support: <https://saferate.com/contact>

## Licence

The contents of this repository are released under the [MIT licence](LICENSE).
The Safe Rate name and logo are trademarks of Safe Rate Inc. and are not covered
by it.
