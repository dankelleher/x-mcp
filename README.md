# X(Twitter) MCP server - OAuth 2.0 Fork

[![smithery badge](https://smithery.ai/badge/x-mcp)](https://smithery.ai/server/x-mcp)

An MCP server to create, manage and publish X/Twitter posts directly through Claude chat.

**This is a fork of [vidhupv/x-mcp](https://github.com/vidhupv/x-mcp) that uses OAuth 2.0 authentication instead of OAuth 1.0a, requiring only a single access token instead of four credentials.**

<a href="https://glama.ai/mcp/servers/jsxr09dktf">
  <img width="380" height="200" src="https://glama.ai/mcp/servers/jsxr09dktf/badge" alt="X(Twitter) Server MCP server" />
</a>

## Quick Setup

### Installing via Smithery

To install X(Twitter) MCP Server for Claude Desktop automatically via [Smithery](https://smithery.ai/server/x-mcp):

```bash
npx -y @smithery/cli install x-mcp --client claude
```

### Manual Installation
1. Clone the repository:
```bash
git clone https://github.com/dankelleher/x-mcp.git
```

2. Install UV globally using Homebrew in Terminal:
```bash
brew install uv
```

3. Create claude_desktop_config.json:
   - For MacOS: Open directory `~/Library/Application Support/Claude/` and create the file inside it
   - For Windows: Open directory `%APPDATA%/Claude/` and create the file inside it

4. Add this configuration to claude_desktop_config.json:
```json
{
  "mcpServers": {
    "x_mcp": {
      "command": "uv",
      "args": [
        "--directory",
        "/path/to/x-mcp",
        "run",
        "x-mcp"
      ],
      "env": {
        "TWITTER_ACCESS_TOKEN": "your_oauth2_access_token"
      }
    }
  }
}
```

5. Get your X/Twitter OAuth 2.0 Access Token:
   - Go to [X API Developer Portal](https://developer.x.com/en/products/x-api)
   - Create a project
   - In User Authentication Settings: 
     - Enable OAuth 2.0
     - Set up with Read and Write permissions, Web App type
     - Add scopes: `tweet.read`, `tweet.write`, `users.read`
   - Set Callback URL to your OAuth handler URL
   - Use OAuth 2.0 Authorization Code Flow with PKCE to obtain an access token
   - **Note**: This fork only requires the OAuth 2.0 access token, not the consumer keys or OAuth 1.0a tokens

6. Update the config file:
   - Replace `/path/to/x-mcp` with your actual repository path
   - Add your X/Twitter OAuth 2.0 access token

7. Quit Claude completely and reopen it

## Usage Examples

* "Tweet 'Just learned how to tweet through AI - mind blown! 🤖✨'"
* "Create a thread about the history of pizza"
* "Show me my draft tweets"
* "Publish this draft!"
* "Delete that draft"

## OAuth 2.0 Changes

This fork simplifies authentication by using OAuth 2.0 instead of OAuth 1.0a:

- **Original**: Required 4 credentials (API Key, API Secret, Access Token, Access Token Secret)
- **This Fork**: Requires only 1 credential (OAuth 2.0 Access Token)
- All API calls use `user_auth=False` parameter to enable OAuth 2.0 authentication
- Supports both `X_ACCESS_TOKEN` and `TWITTER_ACCESS_TOKEN` environment variables

## Troubleshooting

If not working:
- Make sure UV is installed globally (if not, uninstall with `pip uninstall uv` and reinstall with `brew install uv`)
- Or find UV path with `which uv` and replace `"command": "uv"` with the full path
- Verify your OAuth 2.0 access token is correct and has the required scopes
- Check if the x-mcp path in config matches your actual repository location