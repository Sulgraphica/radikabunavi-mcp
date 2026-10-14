# Radikabunavi MCP (ラジ株ナビ MCP)

[![Glama score](https://glama.ai/mcp/connectors/com.radikabunavi/japan-stock-edinet/badges/score.svg)](https://glama.ai/mcp/connectors/com.radikabunavi/japan-stock-edinet)

**日本語の要約:** ラジ株ナビの MCP サーバーです。Claude・ChatGPT・Cursor などの AI から、EDINET（有価証券報告書）と TDnet（適時開示・決算短信）をもとにした日本の上場企業データ（財務、6軸スコア、理想株価、DCF、決算速報、スクリーニングなど）を呼び出せます。このリポジトリはドキュメントのみで、ソースコードは含みません。情報提供のみで、投資助言ではありません。

---

Remote MCP server for Japanese listed-company data, built from EDINET annual securities reports and TDnet timely disclosures. Covers roughly 3,700 listed companies (Prime / Standard / Growth) with up to 10 years of history.

This repository contains **documentation only**. The server is a hosted service; there is no source code here.

## Endpoint

```
https://radikabunavi.com/mcp
```

- Transport: Streamable HTTP
- Authentication (either one):
  - OAuth 2.1 with PKCE and dynamic client registration (used automatically by Claude and ChatGPT; no API key needed)
  - Bearer API key (`Authorization: Bearer rk_...`), issued free from <https://radikabunavi.com/mcp-mypage>

## Connect

Official guides (Japanese):

- Getting started in 3 steps (for beginners): <https://radikabunavi.com/mcp-start>
- Service overview and setup: <https://radikabunavi.com/mcp-service>
- Claude connection guide: <https://radikabunavi.com/mcp-claude-guide>
- ChatGPT connection guide: <https://radikabunavi.com/mcp-chatgpt-guide>
- Use with Claude Code: <https://radikabunavi.com/claude-code-edinet>

Typical setups:

- **Claude / ChatGPT**: add a custom connector with the URL `https://radikabunavi.com/mcp` and sign in when prompted (OAuth).
- **Cursor and other clients that accept a URL plus headers**: point the client at the endpoint and pass your API key.

```json
{
  "mcpServers": {
    "radikabunavi": {
      "url": "https://radikabunavi.com/mcp",
      "headers": {
        "Authorization": "Bearer rk_YOUR_API_KEY"
      }
    }
  }
}
```

The exact config key names differ between clients. Check your client's documentation.

## Tools (22)

| Tool | Description |
|---|---|
| `search_stocks` | Search companies by name or securities code (absorbs hiragana/katakana and full/half-width variants) |
| `get_stock_analysis` | Overall analysis of a stock in one call: financials, ideal price, 6-axis score, industry benchmark, earnings forecast and DCF |
| `list_edinet_stocks` | Coverage, data sources and reference guides |
| `get_edinet_financial_data` | Annual financial data from EDINET filings, with company forecasts from TDnet |
| `get_earnings_forecast` | Company forecasts (next-period results and dividends) extracted from TDnet earnings reports |
| `get_earnings_flash` | Earnings flash from TDnet reports, ordered by attention level |
| `get_timely_disclosures` | TDnet timely disclosures for today or a given date |
| `get_large_holdings` | Large shareholding reports (5% rule) |
| `get_major_shareholders_history` | Time series of the top 10 shareholders from annual securities reports |
| `get_investor_portfolio` | Reverse lookup from an investor to the stocks they hold, built from major shareholder data |
| `get_main_customers` | Major customers (10%+ of consolidated sales) from annual securities reports, and the reverse lookup |
| `get_stock_score` | Radikabunavi 6-axis score (0-100) with an ideal-price summary |
| `get_ideal_price` | Radikabunavi ideal-price model (Mark 3.2, multiplicative) |
| `get_dcf_valuation` | DCF valuation breakdown |
| `get_industry_benchmark` | Median and quartiles per TSE 33-industry group, with a company's position inside its industry |
| `screen_stocks` | Screen all listed companies by financial conditions |
| `screen_by_framework` | Screen by four frames: growth, high dividend, value, earnings recovery |
| `add_to_watchlist` | Add stocks to your watchlist |
| `get_watchlist` | List your watchlist |
| `remove_from_watchlist` | Remove stocks from your watchlist |
| `update_watchlist_note` | Update the note on a watchlist entry |
| `report_issue` | Report a data error (only with the user's consent) |

Tool list taken from the live server card: <https://radikabunavi.com/.well-known/mcp/server-card.json>

## Pricing

| Plan | Price | API calls per day |
|---|---|---|
| Free | 0 JPY | 100 |
| Light | 500 JPY / month | 250 |
| Standard | 1,980 JPY / month | 1,000 |
| Pro | 3,980 JPY / month | 2,000 |

Free covers annual data only. Quarterly (Q1-Q3) earnings data requires Light or above. Watchlist limit: Free 10 stocks, Light 50 stocks (as of 2026-10-15; higher plans are listed on the service page). See <https://radikabunavi.com/mcp-service> for current details.

## Data sources

- EDINET (Financial Services Agency of Japan): annual securities reports
- TDnet (Tokyo Stock Exchange): timely disclosures and earnings reports

J-Quants and Yahoo Finance data are not used.

## Listings

- Official MCP Registry: `com.radikabunavi/japan-stock-edinet`
- Smithery: <https://smithery.ai/servers/sulgraphica/japan-stock-edinet>
- Glama: <https://glama.ai/mcp/connectors/com.radikabunavi/japan-stock-edinet>

`server.json` in this repository mirrors the entry published in the official registry.

## Disclaimer

This service provides information only. It is not investment advice and does not recommend buying or selling any security. Make investment decisions at your own responsibility. Data is derived from public filings and may contain errors or delays.

## Contact

contact@radikabunavi.com

---

Documentation © Radikabunavi

## License

The documentation in this repository is licensed under [CC BY 4.0](LICENSE) (Copyright CLOUD NINE CO., LTD.). The Radikabunavi service, its data, and its logo are not covered by this license.
