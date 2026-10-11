---
layout:         page
title:          What is DAX Lib?
published:      true
date:           2025-08-14
modified:       2026-10-11
order:          /001
next_reading:   true
---

DAX Lib is a website designed to distribute libraries of DAX user-defined functions (UDF). Similar to NuGet, DAX Lib provides a centralized platform where users can discover, share, and download reusable DAX function libraries to enhance their Fabric, Power BI, and Analysis Services semantic models.

# DAX libraries
A DAX library is a collection of DAX user-defined functions that can be reused across different semantic models, promoting best practices and reducing duplication of effort.

## Functions designed for DAX libraries
A DAX user-defined function is candidate for a library if it is model-independent, which means that it has no references to specific tables, columns, or measures within a particular model. When a function has direct dependencies on model elements, it is not suitable for inclusion in a DAX library and must be refactored to remove those dependencies.

Example of a **model-independent function**, good candidate for a DAX library:
```tmdl
function 'Contoso.Lookup.RangeLookup' =
		(
		    search: SCALAR VAL,
		    lookupTable: TABLEREF EXPR,
		    colMin: COLUMNREF EXPR,
		    colMax: COLUMNREF,
		    colTarget: COLUMNREF
		) =>
		    SELECTCOLUMNS (
		        FILTER (
		            lookupTable,
		            colMin <= search && colMax > search
		        ),
		        "@Result", colTarget
		    )
```

Example of a **model-dependent function**, which could be defined in a semantic model to simplify the consumption of a generic function imported from a DAX library:
```tmdl
function PriceLookup =
		(
		    search: SCALAR VAL
		) =>
		    'Contoso.Lookup.RangeLookup' (
		        search,
		        'Price Range',
		        'Price Range'[Min],
		        'Price Range'[Max],
		        'Price Range'[Range]
		    )
```
