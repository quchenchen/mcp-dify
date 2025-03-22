# MCP Fetch Server

## Basic Information
- **Project URL**: https://github.com/modelcontextprotocol/servers/tree/main/src/fetch
- **Developer/Organization**: Model Context Protocol
- **License**: MIT
- **Last Updated**: 2023-11-15

## Project Description
A Model Context Protocol server that provides web content fetching and conversion capabilities for efficient LLM usage. This server enables LLMs to fetch web content from URLs, extract the main content, and convert it into a format that is optimized for processing by language models.

The fetch tool will truncate the response, but by using the `start_index` argument, you can specify where to start the content extraction. This lets models read a webpage in chunks, until they find the information they need.

## Available Tools
- `fetch` - Fetches a URL from the internet and extracts its contents as markdown.
  - `url` (string, required): URL to fetch
  - `max_length` (integer, optional): Maximum number of characters to return (default: 5000)
  - `start_index` (integer, optional): Start content from this character index (default: 0)
  - `raw` (boolean, optional): Get raw content without markdown conversion (default: false)

## Prompts
- **fetch**
  - Fetch a URL and extract its contents as markdown
  - Arguments:
    - `url` (string, required): URL to fetch

## Dify Integration
This MCP server integrates with Dify through the Model Context Protocol, allowing Dify applications to fetch and process web content efficiently. It has been tested and confirmed to work with Dify.

## Installation

Optionally: Install node.js, this will cause the fetch server to use a different HTML simplifier that is more robust.

### Using uv (recommended)

When using [`uv`](https://docs.astral.sh/uv/) no specific installation is needed. We will use [`uvx`](https://docs.astral.sh/uv/guides/tools/) to directly run *mcp-server-fetch*.

### Using PIP

Alternatively you can install `mcp-server-fetch` via pip:

```
pip install mcp-server-fetch
```

After installation, you can run it as a script using:

```
python -m mcp_server_fetch
```

## Configuration

### Configure for Claude.app

Add to your Claude settings:

**Using uvx**
```json
"mcpServers": {
  "fetch": {
    "command": "uvx",
    "args": ["mcp-server-fetch"]
  }
}
```

**Using docker**
```json
"mcpServers": {
  "fetch": {
    "command": "docker",
    "args": ["run", "-i", "--rm", "mcp/fetch"]
  }
}
```

**Using pip installation**
```json
"mcpServers": {
  "fetch": {
    "command": "python",
    "args": ["-m", "mcp_server_fetch"]
  }
}
```

### Customization - robots.txt

By default, the server will obey a website's robots.txt file if the request came from the model (via a tool), but not if the request was user initiated (via a prompt). This can be disabled by adding the argument `--ignore-robots-txt` to the `args` list in the configuration.

### Customization - User-agent

By default, depending on if the request came from the model (via a tool), or was user initiated (via a prompt), the server will use either the user-agent:
```
ModelContextProtocol/1.0 (Autonomous; +https://github.com/modelcontextprotocol/servers)
```
or
```
ModelContextProtocol/1.0 (User-Specified; +https://github.com/modelcontextprotocol/servers)
```

This can be customized by adding the argument `--user-agent=YourUserAgent` to the `args` list in the configuration.

## Debugging

You can use the MCP inspector to debug the server. For uvx installations:

```
npx @modelcontextprotocol/inspector uvx mcp-server-fetch
```

Or if you've installed the package in a specific directory or are developing on it:

```
cd path/to/servers/src/fetch
npx @modelcontextprotocol/inspector uv run mcp-server-fetch
```

## Additional Information
The server provides the following capabilities:
- Fetch content from any public URL
- Extract the main content from web pages, removing unnecessary elements
- Convert HTML content to plain text or markdown format
- Handle various content types and encodings
- Optimize content for efficient processing by LLMs
- Read webpages in chunks using the start_index parameter

This tool is particularly useful for LLM applications that need to access and process web content, such as research assistants, content summarizers, and information extraction tools.
