# IT and Security Notes

## What this is

The Metry MCP server (https://mcp.metry.io) is a hosted API bridge that lets AI assistants query your organization's energy data using natural language. It is read-only, so it cannot create, update, or delete any data in Metry. This guide covers what your IT or security team needs to know before approving its use.

## Getting started

**Network:** Allow outbound HTTPS to mcp.metry.io. No inbound rules are required.

**Authentication:** Users authenticate with their existing Metry credentials via OAuth 2.1. No service accounts, API keys, or shared secrets are required. Tokens are short-lived and scoped to the user's existing Metry permissions.

**Configuration:** IT can deploy the integration in one of three ways depending on AI vendor:

1. Add Metry MCP as a centrally managed agent/connector in your AI platform and control which users can enable it.
2. Allow users to add custom MCP connectors themselves and let them add the server URL (https://mcp.metry.io) directly.
3. For CLI-based tools, allow installation of the relevant CLI on user machines.

The right approach depends on your AI platform's admin controls and your internal policy for third-party connectors.

## Data and security

**What data is accessed:** Energy consumptions and readings (electricity, heat, cooling, water, gas), meter metadata (name, address, EAN, energy type), property/building structure and account information (name, address, type, locale). No personal data is involved beyond the Metry account used to authenticate.

**How it flows:** The AI tool sends a request to the Metry MCP server over HTTPS. The server validates the OAuth token, queries the Metry backend on the user's behalf, and returns the result to the AI tool. The AI tool then uses that result as context for its response.

**What the AI vendor receives:** The AI vendor (e.g. Anthropic, Microsoft, OpenAI, or Google) receives the data returned by the Metry MCP server as part of the conversation context. This is subject to the data handling terms of your AI tool agreement.

**Hosting:** The MCP server runs on AWS in the EU (eu-west-1, Ireland). All traffic is encrypted in transit (TLS). The server stores no credentials and no conversation data.

## Responsibility split

| Area | Metry | IT / Security team | AI vendor |
|---|---|---|---|
| MCP server security and uptime | Yes | | |
| OAuth authorization server | Yes | | |
| Data accuracy in Metry | Yes | | |
| User access rights in Metry | | Yes | |
| Choosing who gets a Metry account | | Yes | |
| AI tool configuration and rollout | | Yes | |
| Internal AI usage policy and governance | | Yes | |
| Prompt formulation and what is asked | | Yes | |
| Output format, presentation, and response time | | | Yes |
| Recommendations and analysis based on output | | | Yes |
| Prompts and conversation data handling | | | Yes |
| AI model data processing and retention | | | Yes |
| Enterprise data processing agreement (DPA) | | Signs with AI vendor | Provides |

Because Metry merely supplies the integration framework and API bridge, AI deployment requires no assessment on Metry's end. IT and security teams (end-users) remain responsible for vetting selected AI providers and governing how internal data is processed or leveraged.

## AI tool considerations

When energy data retrieved from Metry enters an AI conversation, it is subject to that AI vendor's data handling terms. The practical implications per tool:

**Claude (Anthropic):** Native MCP support with OAuth discovery. Data is processed under Anthropic's usage policies. Enterprise accounts exclude customer data from model training by default.

**Microsoft Copilot:** Add the MCP server via Copilot Studio or the MCP connector. Data stays within your Microsoft 365 data residency boundary and is governed by your Microsoft Customer Agreement and DPA.

**ChatGPT (OpenAI):** Supported via OpenAI's tool/connector interface. Data is processed under OpenAI's enterprise or API terms. Team and Enterprise plans exclude your data from training.

**Google Gemini:** Supported via Google extensions and Vertex AI Agent Builder. Data is governed by your Google Workspace or Cloud agreement.

**What the customer must do regardless of tool:**

- Use an enterprise or business tier account with your AI vendor. Personal accounts typically lack data processing agreements and may use your data for model training.
- Ensure your AI vendor's DPA covers the data types Metry returns (operational/commercial energy data).
- Limit Metry account access to users who need it. The MCP server enforces the same permissions as the Metry account used to authenticate.
- Confirm with your AI vendor whether conversation data is retained, and for how long.

## Reporting a vulnerability

Report security vulnerabilities to [feedback@metry.io](mailto:feedback@metry.io) instead of opening a public issue. Include:

- Description of the vulnerability
- Steps to reproduce
- Potential impact

We aim to acknowledge reports within 48 hours. Please do not disclose vulnerabilities publicly until we have had a reasonable opportunity to address them.
