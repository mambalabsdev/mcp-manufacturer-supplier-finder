# Manufacturer and Supplier Finder MCP Server

[![LightNow capabilities](https://lightnow.ai/badge/com.mambabuilt/mcp-manufacturer-supplier-finder)](https://lightnow.ai/servers/com.mambabuilt/mcp-manufacturer-supplier-finder) [![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-manufacturer-supplier-finder/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-manufacturer-supplier-finder) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-manufacturer-supplier-finder%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-manufacturer-supplier-finder&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-manufacturer-supplier-finder)](https://www.npmjs.com/package/@mambalabsdev/mcp-manufacturer-supplier-finder) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-manufacturer-supplier-finder)](https://www.npmjs.com/package/@mambalabsdev/mcp-manufacturer-supplier-finder) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-manufacturer-supplier-finder)](https://github.com/mambalabsdev/mcp-manufacturer-supplier-finder/blob/main/LICENSE) [![mcpservers.org](https://img.shields.io/badge/mcpservers.org-listed-blue)](https://mcpservers.org/servers/mambalabsdev/mcp-manufacturer-supplier-finder)

An MCP server for the Mamba Labs Manufacturer and Supplier Finder actor on Apify. Give it a product and a country. It searches Google for manufacturers, wholesalers, and distributors, reads each company's own website, and returns only the companies whose pages say they make, wholesale, or distribute the product, with the quoted text and the page as evidence.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Your keys](#your-keys)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Directories, marketplaces, and social networks are never returned. Each candidate site is checked by the Mamba Labs Website Phrase and Business Model Classifier, which the actor runs on your Apify account. When nothing qualifies, one free summary row says how many sites were found and checked. All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-manufacturer-supplier-finder": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-manufacturer-supplier-finder"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `find_suppliers` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Find 20 cast iron cookware manufacturers in the United States."
- "Which UK wholesalers sell organic coffee beans? Show me the evidence from their sites."
- "Find private label skin care manufacturers in Germany."

## Tool

`find_suppliers`. One tool. Example arguments:

```json
{
  "product": "corrugated boxes",
  "country": "US",
  "role": "manufacturer",
  "max_results": "20"
}
```

## Inputs

Every buyer facing input of the actor, unchanged. Omitted inputs take the actor's own defaults. Numbers and booleans are sent as strings.

| Input | Type | Description |
|---|---|---|
| `product` | string | What the suppliers make or sell. Required |
| `country` | string | Two letter code, 20 countries. Default US |
| `role` | string | any (default), manufacturer, wholesaler, or distributor |
| `max_results` | string | 1 to 100. Default 20 |
| `require_product_mention` | string | true (default) or false |
| `extra_keywords` | array | Up to 5 extra search words |
| `exclude_domains` | array | Domains never to return |
| `max_charge_usd` | string | Optional cap on the whole run, website checks included |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `supplier-found`, per supplier returned | $0.025 | $0.02375 | $0.0225 | $0.02125 |
| `apify-actor-start`, per run start | $0.001 | $0.001 | $0.001 | $0.001 |
| Website check by the classifier (`domain-classified`), per site checked | $0.0045 | $0.004275 | $0.00405 | $0.003825 |
| Classifier start (`apify-actor-start`), per run | $0.0005 | $0.0005 | $0.0005 | $0.0005 |

About 2 sites are checked for each supplier returned. A summary row is free, and a site that cannot be read is not charged.

## Your keys

The actor needs no key and holds none. Proxy and Google search traffic add nothing to your price: Mamba Labs pays the platform costs of the run.

## Full actor documentation

[apify.com/mambalabs/manufacturer-supplier-finder](https://apify.com/mambalabs/manufacturer-supplier-finder)

## License

MIT. See [LICENSE](LICENSE).
