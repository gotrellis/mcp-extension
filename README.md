# Qore desktop extension

[Qore](https://qore.gotrellis.com) connects Claude to the marketplace and retail-media accounts
your organization has already authorized — Amazon Ads and Seller Central, Walmart, TikTok Shop,
Google Ads, Shopify, MerchantSpring and Jungle Scout. Ask which products drove ad sales last month,
which search terms burned spend with no sales, or how today is tracking against yesterday hour by
hour, and Claude reads the live data and answers.

You sign in with your own Qore account and choose one organization to connect. There is no API key
to copy: the connection reaches exactly the connectors you can reach in Qore, and you can revoke it
at any time from Connected apps.

## Install

Download `qore-mcp-<version>.mcpb` from [Releases](https://github.com/gotrellis/mcp-extension/releases)
and open it — Claude Desktop installs it and takes you through signing in.

## What is in here

Qore MCP is a hosted server at `https://clio.growthvectors.io/mcp`, speaking Streamable HTTP with
OAuth 2.1 and dynamic client registration. [MCPB](https://github.com/modelcontextprotocol/mcpb) has
no remote server type, so this extension is a thin wrapper: a pinned
[`mcp-remote`](https://www.npmjs.com/package/mcp-remote) that Claude Desktop runs over stdio and
that forwards to the hosted endpoint. Sign-in still happens against Qore in your browser.

The tool surface is not declared here. It is derived per organization from the platforms that
organization has connected, which is why `tools_generated` is `true` in the manifest and the listed
tools are illustrative.

## Build

```bash
cd server && npm ci --omit=dev && cd ..
npx @anthropic-ai/mcpb validate .
npx @anthropic-ai/mcpb pack . qore-mcp-1.0.0.mcpb
```

Releases are built by `.github/workflows/release.yml`: bump `version` in `manifest.json`, then push
a matching `v*` tag and the workflow packs the bundle and attaches it to the release.
