# MCP Sequential Thinking

## Basic Information

- **Project URL**: https://github.com/modelcontextprotocol/servers/tree/HEAD/src/sequentialthinking
- **Developer/Organization**: Model Context Protocol
- **License**: MIT
- Project Description

An MCP server implementation that provides a tool for dynamic and reflective problem-solving through a structured thinking process. This server enables LLMs to break down complex problems into sequential steps, analyze each step thoroughly, and build upon previous reasoning to reach comprehensive solutions.

## Dify Integration

This MCP server integrates with Dify through the Model Context Protocol, allowing Dify applications to leverage structured sequential thinking capabilities. It has been tested and confirmed to work with Dify.

## Features

- Break down complex problems into manageable steps
- Revise and refine thoughts as understanding deepens
- Branch into alternative paths of reasoning
- Adjust the total number of thoughts dynamically
- Generate and verify solution hypotheses
- Maintain context and build upon previous reasoning
- Support for dynamic problem-solving with reflection capabilities
- Enable LLMs to tackle multi-step reasoning tasks more effectively
- Improve the quality and transparency of LLM reasoning processes

## Tool

### sequential_thinking

Facilitates a detailed, step-by-step thinking process for problem-solving and analysis.

**Inputs:**

- `thought` (string): The current thinking step
- `nextThoughtNeeded` (boolean): Whether another thought step is needed
- `thoughtNumber` (integer): Current thought number
- `totalThoughts` (integer): Estimated total thoughts needed
- `isRevision` (boolean, optional): Whether this revises previous thinking
- `revisesThought` (integer, optional): Which thought is being reconsidered
- `branchFromThought` (integer, optional): Branching point thought number
- `branchId` (string, optional): Branch identifier
- `needsMoreThoughts` (boolean, optional): If more thoughts are needed

## Use Cases

This tool is particularly useful for:

- LLM applications that require complex reasoning
- Problem-solving assistants
- Decision support systems
- Educational tools that need to demonstrate step-by-step thinking processes
- Multi-step planning tasks
- Situations where context needs to be maintained over multiple steps
- Filtering out irrelevant information
- Planning and design with room for revision
- Analysis that might need course correction
- Problems where the full scope might not be clear initially

## Configuration

### Usage with Claude Desktop

Add this to your `claude_desktop_config.json`:

#### npx

```json
{
  "mcpServers": {
    "sequential-thinking": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-sequential-thinking"
      ]
    }
  }
}
```

#### docker

```json
{
  "mcpServers": {
    "sequentialthinking": {
      "command": "docker",
      "args": [
        "run",
        "--rm",
        "-i",
        "mcp/sequentialthinking"
      ]
    }
  }
}
```

## Building

Docker:

```bash
docker build -t mcp/sequentialthinking -f src/sequentialthinking/Dockerfile .
```

## License

This MCP server is licensed under the MIT License. This means you are free to use, modify, and distribute the software, subject to the terms and conditions of the MIT License. For more details, please see the LICENSE file in the project repository.
