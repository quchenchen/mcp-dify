# Firecrawl MCP Server

## Basic Information
- **Project URL**: https://github.com/mendableai/firecrawl-mcp-server
- **Developer/Organization**: Mendable AI
- **License**: MIT
- **Last Updated**: 2025-03-18

## Project Description
A Model Context Protocol (MCP) server implementation that integrates with Firecrawl for web scraping capabilities. This server enables LLMs to scrape, crawl, search, and extract web content efficiently, with support for JavaScript rendering and batch processing.

Firecrawl MCP Server provides advanced web scraping capabilities for AI applications, allowing models to gather information from the web with features like deep research, content extraction, and smart filtering.

## Available Tools
- `scrape` - Scrapes a URL with JavaScript rendering support
  - `url` (string, required): URL to scrape
  - `viewport` (string, optional): "mobile" or "desktop" (default: "desktop")
  - `include_tags` (array, optional): HTML tags to include in extraction
  - `exclude_tags` (array, optional): HTML tags to exclude from extraction
  
- `search` - Performs web search and extracts content from results
  - `query` (string, required): Search query
  - `num_results` (integer, optional): Number of results to return (default: 5)
  - `extract_content` (boolean, optional): Whether to extract content from search results (default: true)
  
- `crawl` - Discovers and crawls URLs from a starting point
  - `url` (string, required): Starting URL for crawling
  - `max_depth` (integer, optional): Maximum crawl depth (default: 2)
  - `max_pages` (integer, optional): Maximum pages to crawl (default: 10)
  
- `batch_scrape` - Scrapes multiple URLs in batch with rate limiting
  - `urls` (array, required): Array of URLs to scrape
  - `concurrency` (integer, optional): Number of concurrent requests (default: 3)
  - `viewport` (string, optional): "mobile" or "desktop" (default: "desktop")

## Prompts
- **scrape**
  - Scrape a URL with JavaScript rendering support
  - Arguments:
    - `url` (string, required): URL to scrape
    
- **search**
  - Perform web search and extract content from results
  - Arguments:
    - `query` (string, required): Search query
    
- **crawl**
  - Discover and crawl URLs from a starting point
  - Arguments:
    - `url` (string, required): Starting URL for crawling
    
- **batch_scrape**
  - Scrape multiple URLs in batch with rate limiting
  - Arguments:
    - `urls` (array, required): Array of URLs to scrape

## Dify Integration
This MCP server integrates with Dify through the Model Context Protocol, allowing Dify applications to leverage advanced web scraping capabilities. It has been tested and confirmed to work with Dify.

## Installation

### Using npm

```
npm install -g firecrawl-mcp-server
```

After installation, you can run it as a command:

```
firecrawl-mcp-server
```

### Using Docker

```
docker pull mendableai/firecrawl-mcp-server
docker run -i --rm mendableai/firecrawl-mcp-server
```

## Configuration

### Configure for Claude.app

Add to your Claude settings:

**Using npm installation**
```json
"mcpServers": {
  "firecrawl": {
    "command": "firecrawl-mcp-server",
    "args": []
  }
}
```

**Using docker**
```json
"mcpServers": {
  "firecrawl": {
    "command": "docker",
    "args": ["run", "-i", "--rm", "mendableai/firecrawl-mcp-server"]
  }
}
```

### API Key Configuration

For cloud-hosted Firecrawl instances, you'll need to set your API key:

```
FIRECRAWL_API_KEY=your_api_key firecrawl-mcp-server
```

Or using environment variables in Docker:

```
docker run -i --rm -e FIRECRAWL_API_KEY=your_api_key mendableai/firecrawl-mcp-server
```

### Self-hosted Configuration

For self-hosted Firecrawl instances, set the endpoint URL:

```
FIRECRAWL_ENDPOINT=http://your-firecrawl-instance.com firecrawl-mcp-server
```

## Changelog

### [1.7.0] - 2025-03-18

#### Fixed
- Critical bugfix for stdio transport hanging issues with Python clients
- Implemented transport-aware logging that directs logs to stderr when using stdio transport
- Resolves issue #22 where Python clients would hang during initialization or tool execution
- Improves compatibility with non-JavaScript MCP clients

### [1.6.0] - 2025-02-10

#### Added
- Support for mobile/desktop viewport selection
- Smart content filtering with tag inclusion/exclusion
- Credit usage monitoring for cloud API

### [1.5.0] - 2025-01-15

#### Added
- Batch scraping capabilities with built-in rate limiting
- Automatic retries with exponential backoff
- Comprehensive logging system