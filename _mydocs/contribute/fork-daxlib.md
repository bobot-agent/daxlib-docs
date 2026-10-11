---
layout:         page
title:          Contribute Small Libraries to DAX Lib
menu_title:     Small Libraries
published:      true
date:           2025-10-17
modified:       2026-10-11
order:          /03
next_reading:   true
---

For small libraries (a few functions), you can follow these steps to add a new package to DAX Lib.

## **Fork** 

Fork the DAX Lib repository: 

<a href="https://github.com/daxlib/daxlib/fork" class="button" target="_blank">Fork daxlib/daxlib</a>
    
This creates a personal copy of the repository in your GitHub account.

> Do not make changes directly on the `main` branch. Always create a separate branch for each change you want to make. For example, `add-my-package-version-1.0.0`. This keeps your work isolated until it's reviewed and approved.

## Create a folder 

Create a folder for your package in `/packages/`, following the [naming conventions](naming-conventions.md) for both the folder structure and library name. For a library named `Contoso.Conversion` with version `1.0.0`, the folder structure should be `/packages/c/contoso.conversion/1.0.0/`
    
## Create the package

DAX Lib requires the `manifest.daxlib` and `lib/functions.tmdl` files. The `README.md` and `icon.png` files are optional.

```bash
packages/
├── a/
├── .../
├── c/
│   └── contoso.conversion/
│       └── 1.0.0/
│           ├── lib/
│           │   └── functions.tmdl   # Required - Your DAX UDF functions
│           ├── icon.png             # Optional - Icon for your library
│           ├── README.md            # Optional - Docs for your library
│           └── manifest.daxlib      # Required - Declares package properties
├── .../
└── z/
```

> You can use the [DaxLib.Sample](https://github.com/daxlib/daxlib/tree/main/packages/d/daxlib.sample/0.1.6) package as a starting point: copy it, rename it according to your library's name, and then update its contents to match your library.

### manifest.daxlib

*Required:* The package properties in JSON format.

``` json
{
    "$schema": "https://raw.githubusercontent.com/daxlib/daxlib/refs/heads/main/schemas/manifest/1.0.0/manifest.1.0.0.schema.json",
    "id": "Contoso.Conversion",
    "version": "1.0.0",
    "authors": "Contoso",
    "description": "My amazing library",
    "tags": "DAX,UDF",
    "releaseNotes": "New functions",   // optional
    "projectUrl": "https://contoso.github.io/contoso.conversion/", // optional
    "repositoryUrl": "https://github.com/daxlib/daxlib/tree/main/packages/c/contoso.conversion",
    "icon": "/icon.png",    // optional
    "readme": "/README.md"  // optional
}
```

Refer to the [JSON schema](https://github.com/daxlib/daxlib/blob/main/schemas/manifest/1.0.0/manifest.1.0.0.schema.json) for the complete specification of available properties. You can also refer to the example [DaxLib.Sample](https://daxlib.org/package/DaxLib.Sample/#code) package.

### lib/functions.tmdl

*Required:* Contains TMDL definition of the functions within your library. TMDL script must *not* have `CreateOrReplace` keyword.

```tmdl
/// Convert from Celsius(°C) to Fahrenheit(°F)
/// @param {decimal} temperature - The temperature in Celsius
/// @returns The temperature converted to Fahrenheit
function 'Contoso.Conversion.CelsiusToFahrenheit' =
		(
		    temperature: DOUBLE
		) =>
		    ( temperature * ( 9 / 5 ) ) + 32

	annotation DAXLIB_PackageId = Contoso.Conversion

	annotation DAXLIB_PackageVersion = 1.0.0
...
```

#### Naming Convention

There are some guidelines on DAX UDF naming conventions:

- [DAX Lib Naming Conventions](https://docs.daxlib.org/contribute/naming-conventions)
- [SQLBI DAX Naming Conventions](https://docs.sqlbi.com/dax-style/dax-naming-conventions)

#### Annotations

Each function must have these two annotations:

- `DAXLIB_PackageId`: the package name. Use the same value as `id` in `manifest.daxlib`.
- `DAXLIB_PackageVersion`: the package version. Use the same value as `version` in `manifest.daxlib`.

```tmdl
	annotation DAXLIB_PackageId = Contoso.Conversion

	annotation DAXLIB_PackageVersion = 1.0.0
```

### icon.png

*Optional:* icon for library

The icon file must be in PNG format (.PNG), with a maximum size of 100 KB.

### README.md
    
*Optional:* Markdown docs file, with general information about the library, usage instructions, examples, and any notes for users

The file must be in Markdown format (.MD), with a maximum size of 100 KB. For security reasons, only a limited set of Markdown features are supported, and external links may be restricted to trusted domains.

## Submitting Library to DAX Lib

Create a pull request from your fork (`<youraccount>/daxlib`) to `daxlib/daxlib` to publish the library on [daxlib.org](https://daxlib.org/). The pull request must be approved manually by DAX Lib owners/maintainers. After approval, your library is available on [DAX Lib](https://daxlib.org/) for other users to download and use.

> **Packages are immutable**
>
> After DAX Lib accepts a pull request, the package is immutable. To change functions or files, create a new version (for example, from 1.0.0 to 1.1.0). Update the version number in `manifest.daxlib` and in the `DAXLIB_PackageVersion` annotation of each function. Then submit the changes in a new pull request.
