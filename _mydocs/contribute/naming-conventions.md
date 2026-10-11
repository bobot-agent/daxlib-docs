---
layout:         page
title:          Naming Conventions
published:      true
date:           2025-09-20
modified:       2026-10-11
order:          /08
next_reading:   true
---

When creating a new package for DAX Lib, it is important to follow specific conventions to ensure consistency and clarity across the platform. Below are the key guidelines to adhere to when naming your package and its components:

1. **Hierarchical Nomenclature**

    - The package name must follow a hierarchical structure, where the first segment is recommended to identify the publisher or author, and the subsequent segments define the library’s scope.
    - Do not use built-in DAX function names or other DAX reserved keywords as any segment. See **Reserved Keywords** below for reference.
    
    Examples:
     - `Contoso.Conversion` - a library of conversion functions published by Contoso.
     - `Northwind.Math.Geometry` - a library of geometrical math functions published by Northwind.

2. **Package Folder Name** (⚠️ only for Small Libraries)

    > This naming convention only applies to Small Libraries created by forking the DAX Lib repository.
    
    - The folder name for your package should be in lowercase letters and use dots to separate different levels of hierarchy.

      Example: for a package named `Contoso.Conversion`, the folder name should be:

      ```bash
      /packages/c/contoso.conversion/
      ```

3. **Package Name**

    - The name of the package should follow PascalCase naming conventions and use dots to separate different levels of hierarchy, where each word starts with an uppercase letter and there are no spaces or underscores.
    - Exceptions are allowed for well-known acronyms (e.g., `XML`, `JSON`, `SVG`) which can be in uppercase.

      Example: for a package named `Contoso.Conversion`, the name in `manifest.daxlib` should be:
  
      ```json
      {
        "id": "Contoso.Conversion"
        // ...other manifest properties...
      }
      ```

4. **Function Naming**

    - All functions within the package should be prefixed with the package name to avoid naming conflicts.
    - Function names should follow the [DAX naming conventions for user-defined functions](https://docs.sqlbi.com/dax-style/dax-naming-conventions#function-names).

    Example: for a package named `Contoso.Conversion`, a function named `CelsiusToKelvin` should defined as:

    ```yaml
    function 'Contoso.Conversion.CelsiusToKelvin' =
    # ... function implementation
    ```

5. **Reserved Keywords**:

    - Do not use built-in DAX function names or other DAX reserved keywords in the package or function name (e.g. `MEASURE`, `FUNCTION`, `DEFINE`, `FILTER`, `DATE`)
     
      Example of invalid names:
      - `Contoso.Filter` (uses reserved keyword `FILTER`)
      - `Contoso.Conversion.Date` (uses reserved keyword `DATE`)

    - Do not use `Dax.` in the package name (`Dax` as a single word is a reserved keyword in function names). 
    - Do not use `DaxLib.` as a prefix for package name. This prefix is reserved for public open-source libraries of common use. Do not submit pull requests for new libraries using the `DaxLib.` prefix.

6. **Folder Structure** (⚠️ only for Small Libraries)
    > This naming convention only applies to Small Libraries created by forking the DAX Lib repository.
   - The **first level** structure should be a single letter (lowercase) corresponding to the first letter of the package name. This helps reduce the number of items in a single folder and keeps the repository organized.
   - The **second level** should be the package name (lowercase).
   - The **third level** should be the package version.

   Example: for a package named `Contoso.Conversion` with version `1.0.0`, the folder should be:

    ```bash
    /packages/c/contoso.conversion/1.0.0/
    ```

By following these naming conventions, you help maintain a well-organized and easily navigable repository of DAX libraries, making it easier for users to find and utilize the functions they need.