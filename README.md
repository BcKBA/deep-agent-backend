# MCP Servers Setup

This project is configured to use multiple MCP (Model Context Protocol) servers for integrating various AI tools into VS Code via Copilot.

## Configured Servers

### GitHub MCP Server
- **Purpose**: GitHub API integration
- **Package**: `@modelcontextprotocol/server-github`
- **Features**: Repository management, issues, pull requests, API access

### LangChain MCP Server
- **Purpose**: LangChain framework integration
- **Package**: `langchain-mcp`
- **Features**: AI agent development, chain orchestration, tool integration

## Setup Instructions

1. Obtain required tokens:
   - **GitHub Personal Access Token**:
     - Go to GitHub Settings > Developer settings > Personal access tokens
     - Generate a new token with appropriate permissions (e.g., repo, read:org)
   - **LangChain**: No additional token required (uses npm package)

2. Update the MCP configuration:
   - Open `.vscode/mcp.json`
   - Replace `"your_token_here"` with your actual GitHub Personal Access Token

3. Restart VS Code to load the MCP servers.

## Usage

Once configured, you can use the following tools in Copilot chat:

### GitHub Tools
- Searching repositories
- Managing issues and pull requests
- Accessing GitHub API data

### LangChain Tools
- Building and running LangChain chains
- Integrating with various AI models and tools
- Developing AI agents and workflows

## Security Note

Keep your GitHub Personal Access Token secure and do not commit it to version control. Consider using environment variables or VS Code's secret storage for production use.