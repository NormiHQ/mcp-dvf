# Normi — serveur MCP de données immobilières françaises

> Interrogez les ventes DVF, les DPE ADEME et la BDNB depuis claude.ai, ChatGPT, Claude Desktop, Cursor, VS Code ou tout client MCP — connexion OAuth en un clic, ou clé API.

[![npm](https://img.shields.io/npm/v/@normi/mcp-dvf)](https://www.npmjs.com/package/@normi/mcp-dvf)
[![MCP Registry](https://img.shields.io/badge/MCP_Registry-listed-blue)](https://registry.modelcontextprotocol.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## Ce qui distingue Normi

- **DVF nettoyée** : les ventes en bloc, les valeurs aberrantes et les VEFA sont exclues par défaut pour des résultats plus comparables.
- **Données croisées** : les mutations DVF peuvent être enrichies par les DPE ADEME et la BDNB, qui couvre plus de 32 millions de bâtiments.
- **MCP et REST** : les mêmes analyses sont disponibles par serveur MCP ou via l'[API REST](https://normi.fr/docs/api).

## Installation (2 minutes)

### Option A — Connexion OAuth (claude.ai, ChatGPT, Claude Code…)

Ajoutez le serveur distant **`https://mcp.normi.fr/mcp`** dans votre client, puis connectez-vous à Normi et
autorisez l'accès. Aucune clé à copier : si votre compte n'a pas encore de clé API, une clé gratuite
(500 crédits) est créée à la première autorisation. Les crédits sont débités sur la clé active de votre compte.

- **claude.ai, Claude Desktop, mobile, Cowork** — Paramètres → Connecteurs → Ajouter → connecteur personnalisé → collez l'URL. [Guide pas à pas](https://www.normi.fr/docs/install/claude)
- **ChatGPT** — créez une application avec l'URL et l'authentification OAuth (nom libre). [Guide](https://www.normi.fr/docs/install/chatgpt)
- **Claude Code** :

  ```bash
  claude mcp add --transport http normi https://mcp.normi.fr/mcp
  ```

  puis `/mcp` dans Claude Code pour vous connecter.

### Option B — Clé API (STDIO, Cursor, scripts)

Créez un compte sur **[normi.fr](https://normi.fr)** puis une clé dans votre [tableau de bord](https://normi.fr/dashboard/tokens).

**Claude Desktop (STDIO)** — ajoutez ceci à `claude_desktop_config.json` :

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

**Cursor** — ajoutez ceci à `.cursor/mcp.json` pour la connexion distante :

```json
{
  "mcpServers": {
    "normi": {
      "url": "https://mcp.normi.fr/mcp",
      "headers": {
        "Authorization": "Bearer normi_YOUR_TOKEN_HERE"
      }
    }
  }
}
```

L'URL MCP distante `https://mcp.normi.fr/mcp` accepte la connexion OAuth 2.1 ou l'en-tête
`Authorization: Bearer <votre_clé_Normi>`. L'API REST n'accepte que les clés API.

### Posez vos questions

```
"Quels sont les prix au m² à Paris 15ème ?"
"Trouve des comparables pour un T3 de 65m² à Lyon 3ème"
"Évolution des prix à Bordeaux depuis 2020"
```

## Outils principaux

Normi propose 33 outils MCP couvrant DVF, DPE, BDNB, ANIL, SIRENE et les workflows de portefeuille. Le catalogue complet est disponible dans la [documentation MCP Normi](https://normi.fr/docs/mcp).

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

## API REST

Les mêmes analyses sont proposées par l'API REST pour les intégrations sans MCP. [Documentation complète](https://normi.fr/docs/api).

```bash
curl -H "X-API-Key: normi_YOUR_TOKEN" \
  "https://mcp.normi.fr/v1/stats/market?code_postal=75001"
```

## Données

- **DVF** (Demandes de valeurs foncières) : ventes immobilières françaises géocodées, 2014–2025, publiées annuellement par la DGFiP.
- **DPE** : diagnostics de performance énergétique issus de l'ADEME.
- **BDNB** : caractéristiques du bâti, avec plus de 32 millions de bâtiments.
- **Licence DVF** : [Licence Ouverte 2.0](https://www.etalab.gouv.fr/licence-ouverte-open-licence/).

## Links

- [Documentation](https://normi.fr/docs)
- [Catalogue MCP](https://normi.fr/docs/mcp)
- [API Playground](https://normi.fr/docs/api/playground)
- [Tableau de bord](https://normi.fr/dashboard)
- [Paquet npm](https://www.npmjs.com/package/@normi/mcp-dvf)

## License

MIT
