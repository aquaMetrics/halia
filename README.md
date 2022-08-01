
<!-- README.md is generated from README.Rmd. Please edit that file -->

# halia

<!-- badges: start -->

[![R-CMD-check](https://github.com/aquaMetrics/halia/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/aquaMetrics/halia/actions/workflows/R-CMD-check.yaml)
[![Lifecycle:
experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://lifecycle.r-lib.org/articles/stages.html#experimental)
[![Codecov test
coverage](https://codecov.io/gh/aquaMetrics/halia/branch/main/graph/badge.svg)](https://app.codecov.io/gh/aquaMetrics/halia?branch=main)
<!-- badges: end -->

The goal of `halia` R package is to calculate the mixing zone area,
fulfilling these specific steps:

-   Assess the mixing zone area from IQI sampling results (DNA or
    taxonomic).

This package is in an experimental phase. The core algorithm for
calculating the area is unlikely to change, but the functions, and input
and output data structures may change.

## Installation

You can install the development version of `halia` like so:

``` r
install.packages("devtools")
devtools::install_github("aquaMetrics/halia")
```

## Calculate Area

This example shows you how to calculate mixing zone from demo IQI input
data:

``` r
library(halia)
```

``` r
## Run the demo IQI data and return the area of the mixing zone
area <- assess(demo_iqi)
area
#> $`5%`
#> [1] 96914.92
#>
#> $`package version`
#> [1] ‘0.2.0’
#> 
#> $`package date`
#> [1] "2022-07-27"
```

Alternatively, it is possible to to see outputs from each step in the
process. As well as add manual overrides for distance to good status or
bearing for each transect:

``` r
data <- consecutive_stations(demo_iqi)
probs <- probability_non_linear(data$survey_data)
overrides <- override(probs,
                      overrideTransect1 = 100, # transect1 overrides
                      overrideBearing1 = -47)
breachs <- breach(overrides)
areas <- area(breachs)
```
