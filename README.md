
# !! ARCHIVED PACKAGE !! Please read below

The PovcalNet website and API have now been retired, and replaced by the [Poverty and Inequality Platform (PIP)](https://pip.worldbank.org/home). As a result, the `PovcanetR` API client is now longer relevant. Please use the [pipR package](https://github.com/worldbank/pipr) instead to interact with the PIP API. Thanks!

## povcalnetR

<!-- badges: start -->

[![Travis build
status](https://travis-ci.org/worldbank/povcalnetR.svg?branch=master)](https://travis-ci.org/worldbank/povcalnetR)
[![AppVeyor build
status](https://ci.appveyor.com/api/projects/status/github/worldbank/povcalnetR?branch=master&svg=true)](https://ci.appveyor.com/project/worldbank/povcalnetR)
[![Coverage
status](https://codecov.io/gh/worldbank/dkanr/branch/master/graph/badge.svg)](https://codecov.io/github/worldbank/dkanr?branch=master)
[![Lifecycle:
maturing](https://img.shields.io/badge/lifecycle-maturing-blue.svg)](https://www.tidyverse.org/lifecycle/#maturing)
[![CRAN
status](https://www.r-pkg.org/badges/version/povcalnetR)](https://cran.r-project.org/package=povcalnetR)
![CRAN](http://cranlogs.r-pkg.org/badges/povcalnetR?color=brightgreen)

<!-- badges: end -->

The `povcalnetR` package allows R users to compute poverty and
inequality indicators for more than 160 countries and regions from the
World Bank’s database of household surveys. It has the same
functionality as the [PovcalNet
website](http://iresearch.worldbank.org/PovcalNet/home.aspx). PovcalNet
is a computational tool that allows users to estimate poverty rates for
regions, sets of countries or individual countries, over time and at any
poverty line.

PovcalNet is managed jointly by the Data and Research Group in the World
Bank’s Development Economics Division. It draws heavily upon a strong
collaboration with the Poverty and Equity Global Practice, which is
responsible for the gathering and harmonization of the underlying survey
data.

PovcalNet reports the following measures at the chosen poverty line:  
\- Headcount ratio  
\- Poverty Gap  
\- Squared Poverty Gap  
\- Watts index

It also reports these inequality measures:  
\- Gini index  
\- mean log deviation  
\- decile shares

The underlying welfare aggregate is per capita household income or
consumption expressed in 2011 PPP-adjusted USD. Poverty lines are
expressed in daily amounts, while means and medians are monthly.

For more information on the definition of the indicators, [click
here](http://iresearch.worldbank.org/PovcalNet/Docs/dictionary.html)  
For more information on the methodology, [click
here](http://iresearch.worldbank.org/PovcalNet/methodology.aspx)

## Installation

You can install the released version of `povcalnetR` from
[CRAN](https://CRAN.R-project.org) with:

``` r
install.packages("povcalnetR")
```

The development version can be installed from
[GitHub](https://github.com/) with:

``` r
install.packages(c("devtools", "httr"))
devtools::install_github("worldbank/povcalnetR")
```

## Example

This is a basic example that shows how to retrieve some key poverty
statistics from PovcalNet using this package

``` r
library(povcalnetR)
library(dplyr)

df <- povcalnet(country = "ALB")
glimpse(df)
#> Observations: 5
#> Variables: 31
#> $ countrycode    <chr> "ALB", "ALB", "ALB", "ALB", "ALB"
#> $ countryname    <chr> "Albania", "Albania", "Albania", "Albania", "Al...
#> $ regioncode     <chr> "ECA", "ECA", "ECA", "ECA", "ECA"
#> $ coveragetype   <chr> "N", "N", "N", "N", "N"
#> $ year           <dbl> 1996, 2002, 2005, 2008, 2012
#> $ datayear       <dbl> 1996, 2002, 2005, 2008, 2012
#> $ datatype       <chr> "consumption", "consumption", "consumption", "c...
#> $ isinterpolated <dbl> 0, 0, 0, 0, 0
#> $ usemicrodata   <dbl> 1, 1, 1, 1, 1
#> $ ppp            <dbl> 58.16801, 58.16801, 58.16801, 58.16801, 58.16801
#> $ povertyline    <dbl> 1.9, 1.9, 1.9, 1.9, 1.9
#> $ mean           <dbl> 187.8427, 191.9880, 217.0335, 237.5353, 225.2692
#> $ headcount      <dbl> 0.011291240, 0.020473200, 0.011237280, 0.003705...
#> $ povertygap     <dbl> 0.0019115400, 0.0035450460, 0.0018274740, 0.000...
#> $ povertygapsq   <dbl> 0.0005560317, 0.0010593800, 0.0004780857, 0.000...
#> $ watts          <dbl> 0.0023108880, 0.0043677770, 0.0021404260, 0.000...
#> $ gini           <dbl> 0.2701034, 0.3173898, 0.3059566, 0.2998467, 0.2...
#> $ median         <dbl> 165.0867, 158.3630, 184.6848, 198.7757, 195.0467
#> $ mld            <dbl> 0.1191043, 0.1648116, 0.1544128, 0.1488934, 0.1...
#> $ polarization   <dbl> NA, NA, NA, NA, NA
#> $ population     <dbl> 3.168033, 3.051010, 3.011487, 2.947314, 2.900401
#> $ decile1        <dbl> 0.03863, 0.03494, 0.03483, 0.03734, 0.03660
#> $ decile2        <dbl> 0.05289, 0.04859, 0.04920, 0.05137, 0.05193
#> $ decile3        <dbl> 0.06379, 0.05842, 0.05977, 0.06088, 0.06144
#> $ decile4        <dbl> 0.07322, 0.06738, 0.06921, 0.06984, 0.07031
#> $ decile5        <dbl> 0.08380, 0.07653, 0.07988, 0.07912, 0.08084
#> $ decile6        <dbl> 0.09355, 0.08839, 0.09037, 0.08924, 0.09257
#> $ decile7        <dbl> 0.1082, 0.1023, 0.1037, 0.1030, 0.1052
#> $ decile8        <dbl> 0.1247, 0.1198, 0.1213, 0.1193, 0.1229
#> $ decile9        <dbl> 0.1490, 0.1493, 0.1483, 0.1454, 0.1489
#> $ decile10       <dbl> 0.2122, 0.2544, 0.2434, 0.2446, 0.2293
```
