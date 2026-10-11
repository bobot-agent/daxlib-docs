---
layout:         page
title:          Contribute Medium-Large Libraries to DAX Lib
menu_title:     Medium-Large Libraries
published:      true
date:           2025-10-17
modified:       2026-10-11
order:          /04
next_reading:   true
---

When your library starts to grow you might want to connect with your users with GitHub issues, collaborate with others to develop the library or Add documentation site and host (for example) on GitHub Pages. **Medium-Large** libraries allow you to have a repo dedicated to your library to do just this. This page shows how to set one up.

## Create a repository from the template

Create a repository from the `daxlib/lib-quickstart-template` template:

<a href="https://github.com/new?template_name=lib-quickstart-template&template_owner=daxlib" class="button" target="_blank">Use daxlib/lib-quickstart-template Template</a>
    
This creates a personal copy of the repository in your GitHub account. This repo will be dedicated to your library, and should be named after your library (for example, `Contoso/Contoso.Conversion`). If you want to have more than one Medium-Large library, simply create another repo from the template. Follow the [naming conventions](naming-conventions.md) for the library name.

> Just like with Small libraries you will also need a fork of `daxlib/daxlib` (for example, `Contoso/daxlib`). This will be used to generate the pull request to `daxlib/daxlib`.

## Add your library

DAX Lib requires the `manifest.daxlib` and `lib/functions.tmdl` files. The `README.md` and `icon.png` files are optional. These are included in the `src` folder.

```bash
.
├── .github/
│   └── workflows/
│       └── publish-package.yml   # Workflow to create branch on `contoso/daxlib` with your library version
├── src/
│   ├── lib/
│   │   └── functions.tmdl        # Required - Your DAX UDF functions
│   ├── icon.png                  # Optional - Icon for your library
│   ├── README.md                 # Optional - Docs for your library
│   └── manifest.daxlib           # Required - Declares package properties
└── README.md                     # Optional - Info on your library
```

> You can update the `README.md` at the root of the library to give users who visit your repository information about the library, how to contribute, and how to submit issues.

### manifest.daxlib

*Required:* The package properties in JSON format.

``` json
{
    "$schema": "https://raw.githubusercontent.com/daxlib/daxlib/refs/heads/main/schemas/manifest/1.0.0/manifest.1.0.0.schema.json",
    "id": "Contoso.Conversion",
    "version": "0.1.0",
    "authors": "Contoso",
    "description": "My amazing library",
    "tags": "DAX,UDF",
    "releaseNotes": "New functions",   // optional
    "projectUrl": "https://contoso.github.io/contoso.conversion/", // optional Docs site
    "repositoryUrl": "https://github.com/contoso/Contoso.Conversion",
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

	annotation DAXLIB_PackageId = __PLACEHOLDER_PACKAGE_ID__

	annotation DAXLIB_PackageVersion = __PLACEHOLDER_PACKAGE_VERSION__
...
```

#### Naming Convention

There are some guidelines on DAX UDF naming conventions:

- [DAX Lib Naming Conventions](https://docs.daxlib.org/contribute/naming-conventions)
- [SQLBI DAX Naming Conventions](https://docs.sqlbi.com/dax-style/dax-naming-conventions)

#### Annotations

In `functions.tmdl`, use placeholders for the annotation values. The `publish-package.yml` workflow replaces them with the `id` and `version` values from `manifest.daxlib`.

```tmdl
	annotation DAXLIB_PackageId = __PLACEHOLDER_PACKAGE_ID__

	annotation DAXLIB_PackageVersion = __PLACEHOLDER_PACKAGE_VERSION__
```

### icon.png

*Optional:* icon for library

The icon file must be in PNG format (.PNG), with a maximum size of 100 KB.

### README.md
    
*Optional:* Markdown docs file, with general information about the library, usage instructions, examples, and any notes for users

The file must be in Markdown format (.MD), with a maximum size of 100 KB. For security reasons, only a limited set of Markdown features are supported, and external links may be restricted to trusted domains.

## Publish Your Library

We first need to create a Personal Access Token, granting `read/write` permissions on `contoso/daxlib`.

![Generate PAT Token](images/generate-pat-token.png)

We add the token as a secret on `Contoso/Contoso.Conversion`, granting these permission to `Contoso/daxlib`. So that the workflow run from `Contoso/Contoso.Conversion` can create a new branch in `Contoso/daxlib`.

![Add Secret](images/add-secret.png)

Navigate to `actions`, select `publish-package` and `Run workflow`. 

![publish-package](images/publish-package.png)

Once complete, open completed `publish-package` job run, and select the `Open Pull Request`, to open the Pull request Window. 

![Completed publish-package job](images/publish-package-finished.png)

Select `Create pull request` to create a pull request to `daxlib/daxlib`.

![Open Pull Request](images/open-pull-request.png)

The pull request will then be reviewed by the DAX Lib maintainers. If changes are requested during the review:

- Apply the requested fixes to your code in the development repo (`Contoso/Contoso.Conversion`), and commit them to your repository
- Re-run the `publish-package` workflow
- The pull request will be automatically updated

Once your pull request is approved and merged, your library will be automatically published on [daxlib.org](https://daxlib.org/).
