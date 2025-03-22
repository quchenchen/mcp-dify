# MCP Time Server

## Basic Information
- **Project URL**: https://github.com/modelcontextprotocol/servers/tree/main/src/time
- **Developer/Organization**: Model Context Protocol
- **License**: MIT
- **Last Updated**: 2024-05-01

## Project Description
A Model Context Protocol server that provides time and timezone conversion capabilities. This server enables LLMs to get current time information and perform timezone conversions using IANA timezone names, with automatic system timezone detection.

## Dify Integration
This MCP server integrates with Dify through the Model Context Protocol, allowing Dify applications to access current time information and perform timezone conversions. It has been tested and confirmed to work with Dify.

## Available Tools

- `get_current_time` - Get current time in a specific timezone or system timezone.
  - Required arguments:
    - `timezone` (string): IANA timezone name (e.g., 'America/New_York', 'Europe/London')

- `convert_time` - Convert time between timezones.
  - Required arguments:
    - `source_timezone` (string): Source IANA timezone name
    - `time` (string): Time in 24-hour format (HH:MM)
    - `target_timezone` (string): Target IANA timezone name

## Installation

### Using uv (recommended)

When using [`uv`](https://docs.astral.sh/uv/) no specific installation is needed. We will use [`uvx`](https://docs.astral.sh/uv/guides/tools/) to directly run *mcp-server-time*.

### Using PIP

Alternatively you can install `mcp-server-time` via pip:

```bash
pip install mcp-server-time
```

After installation, you can run it as a script using:

```bash
python -m mcp_server_time
```

## Configuration

### Configure for Claude.app

Add to your Claude settings:

**Using uvx**
```json
"mcpServers": {
  "time": {
    "command": "uvx",
    "args": ["mcp-server-time"]
  }
}
```

**Using docker**
```json
"mcpServers": {
  "time": {
    "command": "docker",
    "args": ["run", "-i", "--rm", "mcp/time"]
  }
}
```

**Using pip installation**
```json
"mcpServers": {
  "time": {
    "command": "python",
    "args": ["-m", "mcp_server_time"]
  }
}
```

### Configure for Zed

Add to your Zed settings.json:

**Using uvx**
```json
"context_servers": [
  "mcp-server-time": {
    "command": "uvx",
    "args": ["mcp-server-time"]
  }
],
```

**Using pip installation**
```json
"context_servers": {
  "mcp-server-time": {
    "command": "python",
    "args": ["-m", "mcp_server_time"]
  }
},
```

### Customization - System Timezone

By default, the server automatically detects your system's timezone. You can override this by adding the argument `--local-timezone` to the `args` list in the configuration.

Example:
```json
{
  "command": "python",
  "args": ["-m", "mcp_server_time", "--local-timezone=America/New_York"]
}
```

## Example Interactions

1. Get current time:
```json
{
  "name": "get_current_time",
  "arguments": {
    "timezone": "Europe/Warsaw"
  }
}
```
Response:
```json
{
  "timezone": "Europe/Warsaw",
  "datetime": "2024-01-01T13:00:00+01:00",
  "is_dst": false
}
```

2. Convert time between timezones:
```json
{
  "name": "convert_time",
  "arguments": {
    "source_timezone": "America/New_York",
    "time": "16:30",
    "target_timezone": "Asia/Tokyo"
  }
}
```
Response:
```json
{
  "source": {
    "timezone": "America/New_York",
    "datetime": "2024-01-01T12:30:00-05:00",
    "is_dst": false
  },
  "target": {
    "timezone": "Asia/Tokyo",
    "datetime": "2024-01-01T12:30:00+09:00",
    "is_dst": false
  },
  "time_difference": "+13.0h",
}
```

## Debugging

You can use the MCP inspector to debug the server. For uvx installations:

```bash
npx @modelcontextprotocol/inspector uvx mcp-server-time
```

Or if you've installed the package in a specific directory or are developing on it:

```bash
cd path/to/servers/src/time
npx @modelcontextprotocol/inspector uv run mcp-server-time
```

## Examples of Questions for Claude

1. "What time is it now?" (will use system timezone)
2. "What time is it in Tokyo?"
3. "When it's 4 PM in New York, what time is it in London?"
4. "Convert 9:30 AM Tokyo time to New York time"

## Build

Docker build:

```bash
cd src/time
docker build -t mcp/time .
```

## Contributing

We encourage contributions to help expand and improve mcp-server-time. Whether you want to add new time-related tools, enhance existing functionality, or improve documentation, your input is valuable.

For examples of other MCP servers and implementation patterns, see:
https://github.com/modelcontextprotocol/servers

Pull requests are welcome! Feel free to contribute new ideas, bug fixes, or enhancements to make mcp-server-time even more powerful and useful.

## Additional Information
The server provides the following capabilities:
- Get current time in various formats
- Convert time between different IANA timezones
- Automatic detection of system timezone
- Support for all standard IANA timezone names

This tool is particularly useful for LLM applications that need accurate time information or need to perform timezone calculations.