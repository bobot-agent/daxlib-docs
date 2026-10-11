---
layout:         page
title:          Install the DAX Lib MCP Server
menu_title:     Install
published:      true
date:           2026-10-11
modified:       2026-10-11
order:          /user-guide/mcp/01
next_reading:   true
---

## Requirements

| Requirement | Notes |
|---|---|
| Operating system | Windows x64. Other platforms (Linux, macOS, Windows ARM64) are not available. |
| Node.js | Version 18 or higher. Node.js only starts the server. |
| Power BI Desktop | Necessary to install packages. The target model must have compatibility level 1702 or higher. |
| MCP client | An AI assistant that supports local (stdio) MCP servers. |

The server is a self-contained program. You do not need to install .NET.

## Check the server

Before you configure a client, make sure that the server starts on your computer. Open a terminal and run this command:

```text
npx -y @daxlib/mcp --version
```

The command shows the version of the server. If you see an error, refer to [Troubleshoot the MCP server](troubleshooting.md).

## Configure your MCP client

All MCP clients use the same command to start the server:

```text
npx -y @daxlib/mcp --start
```

Most clients use this configuration format, with the `mcpServers` key:

```json
{
  "mcpServers": {
    "daxlib-mcp": {
      "command": "npx",
      "args": ["-y", "@daxlib/mcp", "--start"]
    }
  }
}
```

VS Code and Visual Studio use the `servers` key instead of `mcpServers`.

### Claude Desktop

1. In Claude Desktop, open **Settings** > **Developer**, then click **Edit Config**.
   On Windows, the configuration file is `%APPDATA%\Claude\claude_desktop_config.json`.
2. Add the `daxlib-mcp` entry to `mcpServers`, as in the example above.
3. Save the file.
4. Quit Claude Desktop completely, then start it again.

### VS Code (GitHub Copilot)

To install the server with one click, open this link:
[Install daxlib-mcp in VS Code](https://vscode.dev/redirect/mcp/install?name=daxlib-mcp&config=%7B%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22%40daxlib%2Fmcp%22%2C%22--start%22%5D%7D).

To configure the server manually, add it to one of these files:

- `.vscode/mcp.json` in your workspace. This file uses the `servers` key.
- The user `mcp.json` file. Run the **MCP: Open User Configuration** command to open it. This file uses the `servers` key.
- `.mcp.json` at the root of your workspace. This file uses the `mcpServers` key.

Example for `.vscode/mcp.json`:

```json
{
  "servers": {
    "daxlib-mcp": {
      "command": "npx",
      "args": ["-y", "@daxlib/mcp", "--start"]
    }
  }
}
```

When VS Code asks if you trust the server, review the configuration and confirm.

### Cursor

Add the `daxlib-mcp` entry with the `mcpServers` key to one of these files:

- `.cursor/mcp.json` in your project, for one project.
- `~/.cursor/mcp.json` in your home folder, for all projects.

### Visual Studio

Add the `daxlib-mcp` entry with the `servers` key to the MCP configuration of Visual Studio.

### Other clients

Use the `mcpServers` configuration above, or the equivalent format of your client. The command is `npx` and the arguments are `-y`, `@daxlib/mcp`, and `--start`.

## Command-line options

```text
npx -y @daxlib/mcp [--start | --version | --help]
```

| Option | Description |
|---|---|
| `--start` | Starts the MCP server on standard input and output. MCP clients use this option. |
| `--version` | Shows the version. |
| `--help`, `-h` | Shows the usage information. |

If you run the command without options, it shows an overview and a configuration example.

## Update the server

To use a specific version of the server, add the version to the package name in the configuration, for example `@daxlib/mcp@0.1.0-beta.4`. Then restart your MCP client.
