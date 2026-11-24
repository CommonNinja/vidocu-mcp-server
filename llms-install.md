# Installing the Vidocu MCP server

Vidocu is a hosted remote server. There is nothing to download, build or run.

1. Add this server to the MCP settings (streamable HTTP):

```json
{
  "mcpServers": {
    "vidocu": {
      "type": "streamableHttp",
      "url": "https://mcp.vidocu.ai/"
    }
  }
}
```

2. On the first tool call the client opens the Vidocu sign-in page (OAuth). The user signs in or creates a free account at https://vidocu.ai and picks a workspace. No API key is needed.

   If the client cannot do OAuth, use a Vidocu API key (`vdo_live_...`, created at https://vidocu.ai/dashboard/developers) instead:

```json
{
  "mcpServers": {
    "vidocu": {
      "type": "streamableHttp",
      "url": "https://mcp.vidocu.ai/",
      "headers": { "Authorization": "Bearer vdo_live_..." }
    }
  }
}
```

3. Check the connection by calling `get_usage`. It returns the workspace's plan and remaining credits.
