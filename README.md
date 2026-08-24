# Normi — French Real Estate Data MCP Server

> Access 17M+ geocoded French property transactions (DVF) from Claude Desktop, Cursor, VS Code, or any MCP client.

[![npm](https://img.shields.io/npm/v/@normi/mcp-dvf)](https://www.npmjs.com/package/@normi/mcp-dvf)
[![MCP Registry](https://img.shields.io/badge/MCP_Registry-listed-blue)](https://registry.modelcontextprotocol.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## Quick Start (2 minutes)

### 1. Get your free API key

Sign up at **[normi.fr](https://normi.fr)** and create a token in your [dashboard](https://normi.fr/dashboard/tokens).

### 2. Configure your MCP client

**Claude Desktop** — edit `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "normi": {
      "command": "npx",
      "args": ["-y", "@normi/mcp-dvf"],
      "env": {
        "NORMI_API_KEY": "normi_YOUR_TOKEN_HERE"
      }
    }
  }
}
```

**Cursor / VS Code (Claude Code)** — add via CLI:

```bash
claude mcp add --transport http normi https://mcp.normi.fr/mcp --header "Authorization: Bearer normi_YOUR_TOKEN"
```

### 3. Start asking questions

```
"Quels sont les prix au m² à Paris 15ème ?"
"Trouve des comparables pour un T3 de 65m² à Lyon 3ème"
"Évolution des prix à Bordeaux depuis 2020"
```

## Key DVF tools

Normi exposes 32 MCP tools across DVF, DPE, BDNB, ANIL, SIRENE and portfolio workflows. The complete,
up-to-date catalog is available in the [Normi MCP documentation](https://normi.fr/docs/mcp).

| Tool | Description | Credits |
|------|-------------|---------|
| `search_property_transactions` | Search transactions by location, type, price, surface | 5 |
| `analyze_market_statistics` | Aggregate stats: median price, price/m², volume | 5 |
| `find_property_comparables` | Find similar properties by proximity and surface | 10 |
| `analyze_price_trends` | Price evolution over time (month/quarter/year) | 10 |
| `compare_locations` | Compare 2-5 locations side by side | 10 |
| `analyze_market_activity` | Transaction volume and seasonality | 10 |
| `get_zonal_price_distribution` | Price statistics by zone (JSON for map visualizations) | 15 |
| `lookup_property_history` | Transaction history for a specific address | 20 |

## REST API

Normi also offers a REST API for non-MCP use cases. [Full documentation](https://normi.fr/docs/api).

```bash
curl -H "X-API-Key: normi_YOUR_TOKEN" \
  "https://mcp.normi.fr/v1/stats/market?code_postal=75001"
```

## Pricing

| Plan | Credits/month | Rate Limit | Price |
|------|--------------|------------|-------|
| **Free** | 500 | 60 req/min | Free |
| **Indie** | 10,000 | 60 req/min | 19 EUR/mo |
| **Agent** | 55,000 | 60 req/min | 49 EUR/mo |
| **Pro** | 175,000 | 60 req/min | 149 EUR/mo |
| **Enterprise** | 500,000 | 120 req/min | 399 EUR/mo |

One-time credit packs also available. [See pricing](https://normi.fr/pricing).

## Data

- **Source**: DVF (Demandes de Valeurs Foncieres) — French government open data
- **Coverage**: All of metropolitan France, 2014-present
- **Volume**: 18M+ geocoded transactions
- **Updates**: Annual (DGFiP publication cadence)
- **License**: [Licence Ouverte 2.0](https://www.etalab.gouv.fr/licence-ouverte-open-licence/)

## Links

- [Documentation](https://normi.fr/docs)
- [API Playground](https://normi.fr/docs/api/playground)
- [Dashboard](https://normi.fr/dashboard)
- [npm package](https://www.npmjs.com/package/@normi/mcp-dvf)

## License

MIT
