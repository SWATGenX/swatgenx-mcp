# SWATGenX MCP Server

The agent-native front door to **[SWATGenX](https://www.swatgenx.com)** — automated,
calibrated SWAT+ watershed modeling for the conterminous United States.

Add it to Claude or any MCP client and a continental watershed-modeling platform becomes a
set of callable tools: search calibrated SWAT+ models, read calibration and held-out
validation scores, query a national groundwater lithology inventory of ~28.8 million depth
intervals, query a national PFAS monitoring inventory, and — with an API key — order and
download watershed models.

- **Endpoint:** `https://www.swatgenx.com/mcp`
- **Transport:** streamable HTTP
- **Full documentation & client setup:** https://www.swatgenx.com/mcp-server

## Connect

```json
{
  "mcpServers": {
    "swatgenx": {
      "type": "http",
      "url": "https://www.swatgenx.com/mcp"
    }
  }
}
```

Six tools need no credentials. To order or download models, send your API key in the
`X-SWATGenX-Api-Key` header (free key with an account at swatgenx.com).

## Tools

| Tool | What it does | Needs |
|---|---|---|
| `search_swat_models` | Browse the example-model catalog (state, size, calibration status) | — |
| `get_model_calibration` | Calibration and held-out validation NSE / PBIAS for one model | — |
| `query_groundwater` | Nearest wells and lithology from the national inventory | — |
| `query_pfas` | National PFAS monitoring inventory by state or analyte | — |
| `request_model` | Preview what SWATGenX would build for a gauge or HUC12 outlet | — |
| `get_access_info` | The access ladder and your current tier | — |
| `order_model` | Order a real SWAT+ build | API key |
| `get_order_status` | Track a build order to completion | API key |
| `list_my_models` | List your build orders | API key |
| `download_model` | Mint a 24-hour download link | API key |

## About

SWATGenX builds physically based SWAT+ and coupled SWAT+/MODFLOW 6 models from NHDPlus HR
hydrography, gSSURGO soils, NLCD land cover and PRISM climate, and calibrates them against
USGS streamflow. The national groundwater inventory this server queries is described in a
preprint under open review at *Earth System Science Data*
([doi:10.5194/essd-2026-527](https://doi.org/10.5194/essd-2026-527)).

The server implementation lives in the main SWATGenX repository; this repository holds the
registry manifest (`server.json`) and the publish workflow.

## License

[MIT](LICENSE)
