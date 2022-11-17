---
title: Packages
description: Zoom
colordes: "#e86e0a"
slug: 05_r_packages
weight: 5
execute:
  error: true
format: hugo
---

Packages are a set of functions and/or data that add functionality to R.

### Looking for packages

-   <a href="https://rdrr.io/find/?repos=cran%2Cbioc%2Crforge%2Cgithub&amp;fuzzy_slug=" target="_blank">Package finder</a>
-   Your peers and the literature

### Package documentation

-   <a href="https://cran.r-project.org/web/packages/available_packages_by_name.html" target="_blank">List of CRAN packages</a>
-   <a href="https://rdrr.io/" target="_blank">Package documentation</a>

### Managing R packages

R packages can be installed, updated, and removed from within R:

``` r
install.packages("package-name")
remove.packages("package-name")
update_packages()
```

### Loading packages

To make a package available in an R session, you load it with the `library()` function.

{{<ex>}}
Example:
{{</ex>}}

``` r
library(readxl)
```

Alternatively, you can access a function from a package without loading it with the syntax: `package::function()`.

{{<ex>}}
Example:
{{</ex>}}

``` r
readxl::read_excel("file.xlsx")
```
