# mcp-dice: A MCP Server for Rolling Dice

A Model Context Protocol (MCP) server that enables Large Language Models (LLMs) to roll dice. It accepts standard dice notation (e.g., `1d20`) and returns both individual rolls and their sum.

## Features

- Supports standard dice notation (e.g., `1d20`, `3d6`)
- Returns both individual rolls and the total sum
- Easy integration with Claude Desktop
- Compatible with MCP Inspector for debugging

## Installation

```shell
# Install using uv
uv pip install mcp-dice
```

## Usage

### Basic Command Line Usage

```shell
# Using uvx
uvx mcp-dice
```

### Input Format

The server accepts a JSON object with a `notation` field:
```json
{
  "notation": "2d6"  // Rolls two six-sided dice
}
```

Example responses:
```json
{
  "rolls": [
    2,
    1
  ],
  "sum": 3,
  "notation": "2d6",
  "timestamp": "2024-12-02T14:47:12.684439"
}
```

## Claude Desktop Configuration

### Location
- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%/Claude/claude_desktop_config.json`

### Examples

<details>
<summary>macOS Configuration</summary>

```json
{
  "mcpServers": {
    "dice_service": {
      "command": "uvx",
      "args": ["mcp-dice"]
    }
  }
}
```
</details>

<details>
<summary>Windows (WSL) Configuration</summary>

```json
{
  "mcpServers": {
    "dice": {
      "command": "wsl",
      "args": [
        "-e",
        "zsh",
        "-lc",
        "uvx mcp-dice"
      ]
    }
  }
}
```

Note: Replace `zsh` with your login shell.
</details>

## Development and Debugging

### Installing Development Dependencies

```shell
# Clone the repository
git clone https://github.com/yourusername/mcp-dice
cd mcp-dice

# Install development dependencies
uv pip install -e ".[dev]"
```

### Running Tests

```shell
uv run pytest
```

### Using MCP Inspector

The [MCP Inspector](https://github.com/modelcontextprotocol/inspector) is a useful tool for debugging your MCP server. Install and run it using npm:

```shell
npx @modelcontextprotocol/inspector uvx mcp-dice
```

### Claude Desktop Configuration for Development

<details>
<summary>macOS Configuration (local dev)</summary>
```json
{
  "mcpServers": {
    "dice_service": {
      "command": "uv",
      "args": [
        "run",
        "--directory",
        "path/to/mcp-dice-repo mcp-dice"
      ]
    }
  }
}
```
</details>

<details>
<summary>Windows (WSL) Configuration (local dev)</summary>

```json
{
  "mcpServers": {
    "dice": {
      "command": "wsl",
      "args": [
        "-e",
        "zsh",
        "-lc",
        "uv run --directory path/to/mcp-dice-repo mcp-dice"
      ]
    }
  }
}
```

Note: Replace `zsh` with your login shell.
</details>
