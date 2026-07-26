# Vidocu MCP Server

> The AI Knowledge Platform as MCP tools. Agents turn videos, PDFs, and slides into
> subtitles, voiceovers, translations, docs, and help articles. Free plan works.

Vidocu is the AI Knowledge Platform for teams that move fast: it turns the materials
you have into the knowledge people need. Product videos, SOPs, how-to guides, help
articles, and training material from one upload.

This is the hosted [Model Context Protocol](https://modelcontextprotocol.io) server
that gives AI agents (Claude, Cursor, Windsurf, and any MCP-aware client) the full
Vidocu API as tools: upload a video or connect source material, generate subtitles
in 65+ languages, add AI voiceover, translate the whole asset, and produce
step-by-step documentation with screenshots, all from conversation. Heavy operations
run async with job polling, so agents can fire work and check back. Hosted and
stateless: nothing to deploy.

## Endpoint

```
https://mcp.vidocu.ai/
```

Remote, streamable HTTP.

## Auth

**OAuth 2.1 (recommended, works on any plan including Free).** The server
advertises Vidocu's authorization server via RFC 9728 protected-resource metadata,
with PKCE and dynamic client registration. Clients that support OAuth connect with
no manual key management, and an agent can produce real output without a credit
card.

**API key (Business plan).** For clients without OAuth support, pass a Vidocu API
key (`vdo_live_...`) as a Bearer token. Mint one at
<https://vidocu.ai/dashboard/developers>.

## Install

Claude Code / CLI (OAuth):

```bash
claude mcp add --transport http vidocu https://mcp.vidocu.ai/
```

Claude Desktop / Cursor / Windsurf (OAuth, any HTTP-transport client):

```json
{
  "mcpServers": {
    "vidocu": {
      "url": "https://mcp.vidocu.ai/"
    }
  }
}
```

API key variant:

```json
{
  "mcpServers": {
    "vidocu": {
      "url": "https://mcp.vidocu.ai/",
      "headers": { "Authorization": "Bearer vdo_live_YOUR_KEY" }
    }
  }
}
```

## Tools (21)

**Videos** - `upload_video`, `get_upload_url`, `list_videos`, `get_video`

**Projects** - `create_project`, `list_projects`, `get_project`, `update_project`,
`delete_project`

**Processing** - `process_video`, `analyze_video`, `get_subtitles`,
`translate_video`, `generate_voiceover`, `generate_article`, `export_video`

**Micro-tools** - `list_tools`, `get_tool`, `execute_tool` (run any of Vidocu's
free tools, like format conversion or subtitle extraction, programmatically)

**Jobs and usage** - `get_job_status`, `get_usage`

## AI Recorder

The platform also includes **AI Recorder** (beta): give Vidocu a help article or a
plain-language instruction and an AI agent opens a real browser, performs the
workflow itself, and records it, returning video, step screenshots, and a written
article from one run.

AI Recorder is not yet exposed through the MCP server or API. Recordings created in
the app land in the same projects these tools operate on, and MCP support is on the
roadmap.

## Pricing

The MCP server works on **every Vidocu plan** with OAuth, including the Free plan
(no credit card). API key auth requires the Business plan. Plans at
<https://vidocu.ai/pricing>.

## Links

- Product: <https://vidocu.ai>
- MCP page: <https://vidocu.ai/mcp>
- MCP docs: <https://vidocu.ai/docs/mcp>
- API docs: <https://vidocu.ai/docs>
- Developers: <https://vidocu.ai/developers>
- Registry: `ai.vidocu/vidocu` on <https://registry.modelcontextprotocol.io>
