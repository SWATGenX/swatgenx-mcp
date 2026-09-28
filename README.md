# SWATGenX MCP Server

The agent-native front door to **[SWATGenX](https://www.swatgenx.com)**: SWAT+ watershed models for any river in the
lower 48 states, built in the cloud from national datasets, with calibration as a separate step you run when you are
ready.

Add it to Claude or any MCP client, and an agent can search the example-model catalog with its calibration and held-out
validation scores, query a national groundwater well inventory and a national PFAS monitoring inventory, preview what a
model of a watershed would contain, read the documentation, and order, track and download a real SWAT+ build under the
same allocations as the web app.

- **Endpoint:** `https://www.swatgenx.com/mcp`
- **Transport:** streamable HTTP (remote; nothing to install)
- **Documentation and client setup:** https://www.swatgenx.com/mcp-server

## Connect

```bash
claude mcp add --transport http swatgenx https://www.swatgenx.com/mcp
```

or, in a client's JSON config:

```json
{ "mcpServers": { "swatgenx": { "type": "http", "url": "https://www.swatgenx.com/mcp" } } }
```

Every call needs a SWATGenX sign-in or an API key. Clients that support MCP authorization sign in with OAuth 2.1 through
swatgenx.com; clients that set headers can send `Authorization: Bearer <your API key>`.

## Tools

From 15 October 2026, the model, data and order tools are part of the paid plans; the documentation tools stay open to
any account.

| Tool | Title | Access from 15 Oct 2026 |
|---|---|---|
| `search_docs` | Search the SWATGenX documentation | any account |
| `get_doc` | Read a SWATGenX documentation chapter | any account |
| `get_engine_info` | Get SWAT+ engine source, build guide and toolchain | any account |
| `get_access_info` | Get access tier and allocations | any account |
| `search_swat_models` | Search SWAT+ example models | paid plan |
| `get_model_calibration` | Get model calibration results | paid plan |
| `query_groundwater` | Query national groundwater wells | paid plan |
| `query_pfas` | Query PFAS monitoring (US or worldwide) | paid plan |
| `request_model` | Preview a watershed model build | paid plan |
| `order_model` | Order a SWAT+ watershed model | paid plan |
| `get_order_status` | Get build order status | paid plan |
| `list_my_models` | List your model orders | paid plan |
| `download_model` | Get a model download link | paid plan |

## About

SWATGenX builds SWAT+ models for a USGS gauge, a HUC12 outlet or a HUC8 basin from NHDPlus HR hydrography, gSSURGO
soils, NLCD land cover and PRISM weather, with an optional steady-state MODFLOW 6 groundwater model. Calibration against
USGS streamflow is a separate step you run when you are ready. Its engine runs SWAT+ and MODFLOW 6 two-way, daily.

The national groundwater inventory is described in [doi:10.5194/essd-2026-527](https://doi.org/10.5194/essd-2026-527).

The server implementation lives in the main SWATGenX repository; this repository holds the registry manifest
(`server.json`) and the publish workflow.

## License

[MIT](LICENSE)
