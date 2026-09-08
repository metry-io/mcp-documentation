# Metry connector for Claude

Metry is a Nordic energy data platform used by real estate owners, property managers, and energy managers to collect and normalize metered consumption data across a portfolio.

The Metry connector gives Claude read access to your organization's meters and consumption data so you can ask questions, generate reports, and analyze energy use in plain language.

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
