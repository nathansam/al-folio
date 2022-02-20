---
layout: page
title: datefixR
description: Fix Really Messy Dates in R
img: assets/img/sticker.png
importance: 1
category: Software
github: "https://www.github.com/nathansam/datefixR"
---

<style type="text/css">
.sidebar {
    height: 100%;
    width: 250px;
    float: right;
    top: 10;
    padding-left: 20px;
    padding-right: 20px;
}
.sidebar div {
    padding: 40px;
    display: block;
    float: left; 
}
</style>



<div class = "sidebar">
{% include figure.html path="assets/img/sticker.png" class="img-fluid rounded z-depth-1" zoomable=true%}
</div>


<!-- badges: start -->

[![R build
status](https://github.com/nathansam/datefixR/workflows/R-CMD-check/badge.svg)](https://github.com/nathansam/datefixR/actions)
[![codecov](https://codecov.io/gh/nathansam/datefixR/branch/main/graph/badge.svg?token=lb83myWBXt)](https://app.codecov.io/gh/nathansam/datefixR)
[![CRAN_Status_Badge](https://www.r-pkg.org/badges/version/datefixR)](https://cran.r-project.org/package=datefixR)
![Top
language](https://img.shields.io/github/languages/top/nathansam/datefixR)
[![License:
GPL-3](https://img.shields.io/badge/License-GPL3-green.svg)](https://opensource.org/licenses/GPL-3.0)
[![CRAN RStudio mirror downloads](https://cranlogs.r-pkg.org/badges/grand-total/datefixR?color=blue)](https://r-pkg.org/pkg/datefixR)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.5655311.svg)](https://doi.org/10.5281/zenodo.5655311)
<!-- badges: end -->

`datefixR` is designed to standardize messy date data, such as dates
entered by different people via text boxes, by converting the dates to
R’s Date data type.

This package arose from my own fights with messy date data where dates
were written in many different formats e.g 01-jan-15, 2015 04 02,
10/12/2010 and more.

## Installation instructions

`datefixR` is now available on CRAN.

{% highlight r %}
install.packages("datefixR")
{% endhighlight %}


The most up-to-date (hopefully) stable version of `datefixR` can be
installed via

{% highlight r %}
if (!require("remotes")) install.packages("remotes")
remotes::install_github("nathansam/fixdateR")
{% endhighlight %}

If you wish to live on the cutting edge of `datefixR` development, then
the development version can be installed via

{% highlight r %}
if (!require("remotes")) install.packages("remotes")
remotes::install_github("nathansam/datefixR", "devel")
{% endhighlight %}

### Usage

{% highlight r %}
library(datefixR)
bad.dates <- data.frame(id = seq(5),
                        some.dates = c("02/05/92",
                                       "01-04-2020",
                                       "1996/05/01",
                                       "2020-05-01",
                                       "02-04-96"),
                        some.more.dates = c("2015",
                                            "02/05/00",
                                            "05/1990",
                                            "2012-08",
                                            "jan 2020")
                        )
fixed.df <- fix_dates(bad.dates, c("some.dates", "some.more.dates"))
knitr::kable(fixed.df)
{% endhighlight %}

|  id | some.dates | some.more.dates |
|----:|:-----------|:----------------|
|   1 | 1992-05-02 | 2015-07-01      |
|   2 | 2020-04-01 | 2000-05-02      |
|   3 | 1996-05-01 | 1990-05-01      |
|   4 | 2020-05-01 | 2012-08-01      |
|   5 | 1996-04-02 | 2020-01-01      |

By default, `datefixR` imputes missing days of the month as 01, and
missing months as 07 (July). However, this behavior can be modified via
the `day.impute` or `month.impute` arguments.

{% highlight r %}
 example.df <- data.frame(example = "1994")

fix_dates(example.df, "example", month.impute = 1)
#>      example
#> 1 1994-01-01
{% endhighlight %}

Functions in `datefixR` assume day-first instead of month-first when
day, month, and year are all given (unless year is given first). However
this behavior can be modified by passing `format = "mdy"` to function
calls.

### Limitations

The package is written solely in R and seems fast enough for my current
use cases (a few hundred rows). However, I may convert the core for loop
to C++ in the future if I (or others) need it to be faster.

### Citation

If you use this package in your research, please consider citing
`datefixR`! An up-to-date citation can be obtained by running

{% highlight r %}
citation("datefixR")
{% endhighlight %}
