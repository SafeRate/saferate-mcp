# Connecting other clients

The server is remote, so there is nothing to install. Point a client that
supports Streamable HTTP at `https://mcp.saferate.com/mcp`.

## Cursor, Windsurf and other `mcpServers` clients

[`mcp.json`](mcp.json):

```json
{
	"mcpServers": {
		"saferate": {
			"url": "https://mcp.saferate.com/mcp"
		}
	}
}
```

## VS Code

[`vscode-mcp.json`](vscode-mcp.json), saved as `.vscode/mcp.json`:

```json
{
	"servers": {
		"saferate": {
			"type": "http",
			"url": "https://mcp.saferate.com/mcp"
		}
	}
}
```

## Clients that only run local (stdio) servers

Bridge with [`mcp-remote`](https://github.com/geelen/mcp-remote) (MIT):

```json
{
	"mcpServers": {
		"saferate": {
			"command": "npx",
			"args": ["-y", "mcp-remote", "https://mcp.saferate.com/mcp"]
		}
	}
}
```

## Signing in

The 17 public tools need no credentials. The five tools that act on a shopper's
own application ask for Safe Rate sign-in (OAuth) when they are called; the
client finds the authorization server through
`https://mcp.saferate.com/.well-known/oauth-protected-resource`.
