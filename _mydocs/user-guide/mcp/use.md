---
layout:         page
title:          Use the DAX Lib MCP Server
menu_title:     Use
published:      true
date:           2026-10-11
modified:       2026-10-11
order:          /user-guide/mcp/02
next_reading:   true
---

Write your requests to the assistant in natural language. The assistant selects the applicable [MCP tool](tools.md). This page shows a typical workflow and example prompts.

## Typical workflow

1. **Find a package.** If you do not know the exact package id, ask the assistant to search DAX Lib.
2. **Select a package.** The assistant shows the results. You select the package.
3. **Examine the package.** Ask for the details or the README to see the functions and how to use them.
4. **Open your model.** Open the target model in Power BI Desktop. Make sure that the compatibility level is 1702 or higher.
5. **Select the target model.** The assistant lists the open Power BI Desktop instances. You select one, even if only one is open.
6. **Install the package.** Approve the install request in your MCP client.
7. **Save your file.** Save the file in Power BI Desktop. The server does not save it.

## Example prompts

### Search

- "Search DAX Lib for packages that generate SVG images."
- "Find DAX Lib packages for date calculations. Show only stable versions."
- "List all packages on DAX Lib."

### Examine a package

- "Show the details of DaxLib.SVG."
- "Which versions of DaxLib.SVG are available?"
- "Show the README of DaxLib.SVG."

### Install

- "List the Power BI Desktop models currently open."
- "Install DaxLib.SVG into the Sales Report model."
- "Install version 2.0.0 of DaxLib.SVG into the model on localhost:51542."

### Use the functions

After the installation, you can ask the assistant to help you use the functions. For example:

- "Using the README of DaxLib.SVG, write a measure that shows a bar for each product."

## Things to know

- **Versions.** If you do not specify a version, the server uses the latest published version. This version can be a prerelease. The assistant must tell you the version before it installs the package. To install a stable version, specify the version.
- **Replaced functions.** The installation replaces functions that have the same name. Other model objects do not change.
- **Approval.** The server does not ask for confirmation itself. Your MCP client asks you to approve the install tool call. Read the tool arguments before you approve.
- **Author content.** Package descriptions, release notes, and README files come from the package authors, not from DAX Lib. Examine them before you use the functions.
