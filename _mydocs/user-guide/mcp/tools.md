---
layout:         page
title:          DAX Lib MCP Tools Reference
menu_title:     Tools Reference
published:      true
date:           2026-10-11
modified:       2026-10-11
order:          /user-guide/mcp/03
next_reading:   true
---

The DAX Lib MCP server has five tools. Four tools only read data. The `install_package` tool changes a model.

| Tool | Read only | Description |
|---|---|---|
| [`search_packages`](#search_packages) | Yes | Searches the DAX Lib catalog. |
| [`get_package`](#get_package) | Yes | Gets the details of a package. |
| [`get_package_readme`](#get_package_readme) | Yes | Gets the README of a package version. |
| [`list_local_instances`](#list_local_instances) | Yes | Lists the Power BI Desktop instances on your computer. |
| [`install_package`](#install_package) | No | Installs a package into a model open in Power BI Desktop. |

## search_packages

Searches DAX Lib and returns a list of packages, one page at a time. For each package, the result shows the id, the latest version, the total downloads, the description, and if a README is available.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `query` | string | No | `""` | A short search keyword, for example `svg`. Add the prefix `packageid:` to find an exact package id. An empty string lists all packages. |
| `limit` | integer | No | `25` | The maximum number of packages on each page. Range: 1–100. Values out of range change to the nearest limit. |
| `skip` | integer | No | `0` | The number of packages to skip, for paging. Negative values change to 0. |
| `includePrerelease` | boolean | No | `true` | Includes packages whose latest version is a prerelease. |

The query is matched as one substring. If there are no results for a query with many words, use one keyword. If there are more results, the response gives the `skip` value for the next page.

## get_package

Gets the details of a package: id, version, description, authors, owners, tags, publication date, download count of the version, README availability, links (gallery, project, and repository), release notes, and all published versions (newest first). This tool does not return DAX code.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `id` | string | Yes | — | The exact package id, for example `DaxLib.SVG`. Not case-sensitive. |
| `version` | string | No | Latest version | The exact package version, for example `2.0.0`. If you do not specify it, the tool uses the latest published version, prerelease included. |

## get_package_readme

Gets the README of a package version as a Markdown resource. The README comes from the package author.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `id` | string | Yes | — | The exact package id, for example `DaxLib.SVG`. Not case-sensitive. |
| `version` | string | No | Latest version | The exact package version. If you do not specify it, the tool uses the latest published version, prerelease included. |

If the package version has no README, the tool returns a message.

## list_local_instances

Lists the Power BI Desktop instances that run on your computer. This tool has no parameters.

For each instance, the result shows:

| Field | Description |
|---|---|
| `processId` | The process id of the instance. |
| `port` | The local port of the instance. |
| `startTime` | The time when the instance started. |
| `parentProcessWindowTitle` | The window title of Power BI Desktop, usually the file name. Two instances can have the same title. |
| `dataSource` | The connection identifier, in `host:port` format (for example `localhost:51542`). Use this value to identify the instance. |

The tool shows only Power BI Desktop instances.

## install_package

Installs a package into a model open in a local Power BI Desktop instance. The tool adds the user-defined functions of the package to the model. If a function with the same name exists, the tool replaces it. The tool does not change other model objects. If you run the tool again with the same arguments, you get the same result.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `id` | string | Yes | — | The exact package id, for example `DaxLib.SVG`. Not case-sensitive. |
| `dataSource` | string | Yes | — | The target instance in `host:port` format, exactly as `list_local_instances` returns it. You must select it. |
| `version` | string | No | Latest version | The exact package version. If you do not specify it, the tool uses the latest published version, prerelease included. |

The tool does these steps in sequence and stops at the first error:

1. Finds the Power BI Desktop instance that has the `dataSource` value.
2. Finds the package and the version.
3. Downloads the package.
4. Reads the functions of the package.
5. Connects to the instance, makes sure that it has one model with compatibility level 1702 or higher, adds the functions, and saves the changes to the model.

If the installation is successful, the result shows the model name and the number of functions that the tool added or replaced. The tool does not save the Power BI Desktop file.

For error messages, refer to [Troubleshoot the MCP server](troubleshooting.md).
