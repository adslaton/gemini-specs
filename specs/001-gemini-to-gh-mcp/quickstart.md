# Quickstart: GitHub Remote MCP Integration

**Date**: 2025-09-24

This guide explains how to configure and use the GitHub Remote MCP integration in the Gemini CLI.

## Configuration

1.  **Create a configuration file.** Create a JSON file (e.g., `mcp_config.json`) with the following content:

    ```json
    {
      "url": "<server-url>",
      "token": "<your-token>"
    }
    ```

2.  **Configure the MCP server in Gemini.** Use the `gemini mcp config` command to set the server configuration from the file:

    ```bash
    gemini mcp config --config-file mcp_config.json
    ```

## Usage

Once the MCP server is configured, you can access repositories that require MCP by providing the repository URL to the relevant Gemini commands.

For example, to list the files in a repository:

```bash
gemini list --repo <repository-url>
```
