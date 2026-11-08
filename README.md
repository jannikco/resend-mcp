# Resend MCP server

Inspect verified sending domains and explicitly submit a transactional email.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `RESEND_API_KEY`



Credential help: https://raw.githubusercontent.com/resend/resend-openapi/main/resend.yaml

## Provider setup

Use your own scoped Resend API key and verified sender domain. Only send to recipients you are authorized to contact. Provider webhook events determine delivery, not the initial API ID.

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call resend_list_domains '{}'
```

## Use with an MCP client

Launch `node /absolute/path/resend-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| resend_list_domains | Read | List sending domains and inspect their verification status. |
| resend_send_email | Explicit approval required | Submit a single email; returned ID is not a delivery receipt. |

## Concrete workflow

Inspect verified sending domains and explicitly submit a transactional email.

1. resend_list_domains
2. resend_send_email

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=resend&integration=resend-mcp&utm_source=github&utm_campaign=github-resend-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/resend/).

## Provenance and maintenance

- https://raw.githubusercontent.com/resend/resend-openapi/main/resend.yaml

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
