# SWATGenX MCP Server

The agent-native front door to **[SWATGenX](https://www.swatgenx.com)**: SWAT+ watershed models for any river in the
lower 48 states, built in the cloud from national datasets, with calibration as a separate step you run when you are
ready.

Add it to Claude or any MCP client, and an agent can search the example-model catalog with its calibration and held-out
validation scores, query a national groundwater well inventory and a national PFAS monitoring inventory, preview what a
model of a watershed would contain, read the documentation, and start, track and download a real SWAT+ build under the
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

Connecting and listing the tools need no sign-in. Every tool call needs a SWATGenX sign-in or an API key: clients that
support MCP authorization sign in with OAuth 2.1 through swatgenx.com; clients that set headers can send
`Authorization: Bearer <your API key>`.

## Tools

From 15 October 2026, the model, data and build tools need model access, and accounts are by invitation. The
documentation, access and engine-info tools stay open to any account.

| Tool | Title | Access from 15 Oct 2026 |
|---|---|---|
| `search_docs` | Search the SWATGenX documentation | any account |
| `get_doc` | Read a SWATGenX documentation chapter | any account |
| `get_engine_info` | Get SWAT+ engine source, build guide and toolchain | any account |
| `get_access_info` | Get access level and allocations | any account |
| `search_swat_models` | Search SWAT+ example models | model access |
| `get_model_calibration` | Get model calibration results | model access |
| `query_groundwater` | Query national groundwater wells | model access |
| `query_pfas` | Query PFAS monitoring (US or worldwide) | model access |
| `request_model` | Preview a watershed model build | model access |
| `order_model` | Build a SWAT+ watershed model | model access |
| `get_order_status` | Get model build status | model access |
| `list_my_models` | List your models and builds | model access |
| `download_model` | Get a model download link | model access |

## About

SWATGenX builds SWAT+ models for a USGS gauge, a HUC12 outlet or a HUC8 basin from NHDPlus HR hydrography, gSSURGO
soils, NLCD land cover and PRISM weather. A groundwater study (offered in Michigan Lower Peninsula, Indiana, Minnesota,
Ohio, Wisconsin) also builds a steady-state MODFLOW 6 groundwater model. Calibration against USGS streamflow is a
separate step you run when you are ready.
Daily two-way SWAT+/MODFLOW 6 coupling is in the engine, not yet in an automatic build.

The national groundwater inventory is described in [doi:10.5194/essd-2026-527](https://doi.org/10.5194/essd-2026-527).

The server implementation lives in the main SWATGenX repository; this repository holds the registry manifest
(`server.json`) and the publish workflow.

## License

[MIT](LICENSE)
