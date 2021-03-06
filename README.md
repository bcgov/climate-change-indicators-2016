
<!-- README.md is generated from README.Rmd. Please edit that file -->

# cccharts

[![img](https://img.shields.io/badge/Lifecycle-Retired-d45500)](https://github.com/bcgov/repomountie/blob/master/doc/lifecycle-badges.md)[![Travis-CI
Build
Status](https://travis-ci.org/bcgov/cccharts.svg?branch=master)](https://travis-ci.org/bcgov/cccharts)[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

## Overview

`cccharts` is an R package to plot climate change indicator data for
British Columbia. It is essentially a wrapper on top of `ggplot2` code.

The package was developed and used to generate supporting data
visualizations for a set of climate change indicators published on
[Environmental Reporting BC
in 2017](https://www2.gov.bc.ca/gov/content/environment/research-monitoring-reporting/reporting/environmental-reporting-bc/climate-change-indicators).

## Installation

The package is not available on CRAN, but can be installed from GitHub
using the [devtools](https://github.com/hadley/devtools) package:

    # install.packages("devtools")
    devtools::install_github("bcgov/cccharts")

## Features

### Three Plot Types

`cccharts` produces three types of plots:

  - Color-coded point (or bar chart) estimates with upper and lower
    confidence intervals (if available) (`plot_estimates`).
  - Color-coded maps of B.C. with the estimates for Ecoprovinces or
    Stations (`map_estimates`).
  - Raw data with estimated trend lines (`plot_fit`).

Examples of the three types of plots are presented below.

To get more information on the arguments that a function takes type for
example `?plot_estimates`.

### PNG Files and `ggplot` Objects

The three base functions return `ggplot` objects which can be modified
prior to plotting. The higher level wrappers `plot_estimates_pngs`,
`map_estimates_pngs` etc automatically save the plots to png files in a
subdirectory of the folder `cccharts` in the working directory. They
also return a list of the `ggplot` objects in case the users wishes to
manipulate them further.

### Color Scheme

The default color scheme is a *diverging* BrBG Brewer
[palette](http://colorbrewer2.org/#type=diverging&scheme=BrBG&n=11). The
user can override the color scheme for the `plot_estimates` or
`map_estimates` functions by setting the `low`, `mid`, and `high`
arguments. To switch to a *sequential* color scheme simply set `mid =
NULL`. To make all points the same color (and suppress a color legend)
simply set `low` and `high` at the same value.

### Data

`cccharts`pulls climate change indicator data from the [BC Data
Catalogue](https://catalogue.data.gov.bc.ca/dataset?download_audience=Public).
The source data sets are licensed under the [Open Government License -
British
Columbia](http://www2.gov.bc.ca/gov/content?id=A519A56BC2BF44E4A008B33FCF527F61).

Type `data()` to see the available datasets or for example type `?snow`
for more information on the snow data.

## Usage

``` r
library(cccharts)
#> Loading required package: ggplot2
plot_estimates(data = cccharts::sea_surface_temperature_station, x = "Season", facet = "Station")
```

![](README-unnamed-chunk-2-1.png)<!-- -->

``` r
map_estimates(data = cccharts::sea_level_station, station = TRUE, bounds = c(0.1,0.7,0,0.55))
#> Warning in seq.default(.limits[1], .limits[2], length = guide$nbin):
#> partial argument match of 'length' to 'length.out'
```

![](README-unnamed-chunk-3-1.png)<!-- -->

``` r
plot_fit(data = dplyr::filter(cccharts::flow_station_discharge, Term == "Medium", Statistic == "Mean", Season == "Annual"), observed = cccharts::flow_station_discharge_observed, free_y = TRUE, facet = "Station")
```

![](README-unnamed-chunk-4-1.png)<!-- -->

To generate the plot files (creates a folder in the working directory
called `cccharts`).

    library(cccharts)
    demo("cccharts", ask = FALSE)

## Getting Help or Reporting an Issue

To report bugs/issues/feature requests, please file an
[issue](https://github.com/bcgov/rcaaqs/issues/).

## How to Contribute

If you would like to contribute to the package, please see our
[CONTRIBUTING](CONTRIBUTING.md) guidelines.

Please note that this project is released with a [Contributor Code of
Conduct](CODE_OF_CONDUCT.md). By participating in this project you agree
to abide by its terms.

## License

    Copyright 2016 Province of British Columbia
    
    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at 
    
       http://www.apache.org/licenses/LICENSE-2.0
    
    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

This repository is maintained by [Environmental Reporting
BC](http://www2.gov.bc.ca/gov/content?id=FF80E0B985F245CEA62808414D78C41B).
Click [here](https://github.com/bcgov/EnvReportBC) for a complete list
of our repositories on GitHub.
