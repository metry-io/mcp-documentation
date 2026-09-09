![Metry MCP](header_mcp.png)

# AI Ready data with Metry MCP

## What is MCP?

The Model Context Protocol (MCP) is an open standard developed by Anthropic that provides a standardized way for AI applications to communicate with external systems. You can think of MCP as a universal connector that allows AI assistants to securely access and interact with various resources such as databases, APIs, and other external platforms.


## About Metry

Metry is an energy data platform used by real estate owners, property managers, and energy managers to collect and normalize metered consumption data across a portfolio.

Metry's MCP server acts as a bridge between your AI tools and Metry's energy data platform. Once you connect the MCP server to your AI tool, you can use the prompt interface to initiate actions using the tools made available by the Metry MCP server. You can ask questions, generate reports, and analyze energy use in plain language.

## What you need before you connecting

- A Metry account with access to at least one organization.
- The "Properties and Buildings" plan to browse your organization's property and building structure. All other features work on any plan.
- A code editor, CLI or application that supports MCP servers.

## What you can do

- Ask natural-language questions about energy consumption across a property portfolio: "How much electricity did we use in Q1 compared to last year?"
- Identify which buildings, properties, or individual meters consume the most of a specific energy type (electricity, heat, cooling, water, gas, and more).
- Break down building-level consumption by area type (common area, tenant area, other) for lease accounting and sustainability reporting.
- Browse how meters are organized into regions, properties, and buildings to scope analysis to a specific part of the portfolio.
- Spot anomalies by fetching hourly or daily meter data and comparing periods.

## What you need before connecting

- A Metry account with access to at least one organization.
- The "Properties and Buildings" plan to browse your organization's property and building structure. All other features work on any plan.

## Available tools

| Tool | What it does |
| --- | --- |
| `get_organization_overview` | Summary of the whole organization: total meters, counts by energy type and status, and the top level of the property tree. Start here for any broad question. |
| `get_meters` | Search and list meters with filters for energy type, status, name, EAN, and location in the tree. Supports paging. |
| `get_meter` | Full details for a single meter by id. |
| `get_current_account` | The account and organization tied to the current session. |
| `get_organization_structure` | The organization's property tree: regions, properties, buildings, and spaces, with meter counts at each level. Requires the Properties and Buildings plan. |
| `get_tree_node` | Full details for a single property, building, or space node, including address, area, energy class, and sector. |
| `get_consumption` | Consumption time series for one or more meters, or for a tree node, at hourly, daily, or monthly granularity. Supports aggregation across meters and unit conversion. |
| `get_asset_consumption` | Monthly energy consumption for a building or property, split into common area, tenant area, and other area. |

## Data access

The connector reads data only. It does not create, update, or delete anything in Metry.

## How to connect

Sign in with your Metry credentials when prompted. The connector uses OAuth and requires no manual token setup.

### Adding it to an MCP client

For web or desktop applications, use `https://mcp.metry.io` as the server URL when adding a custom connector.

For clients configured via JSON, point at the server URL. The server advertises its authorization server through Protected Resource Metadata, so a spec-compliant client discovers the OAuth flow automatically after the first 401.

```json
{
    "mcpServers": {
        "metry": {
            "type": "http",
            "url": "https://mcp.metry.io"
        }
    }
}
```

## Questions and feedback

For questions or feedback, reach us at [feedback@metry.io](mailto:feedback@metry.io).
