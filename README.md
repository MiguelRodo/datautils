
<!-- README.md is generated from README.Rmd. Please edit that file -->

# datautils

<!-- badges: start -->
<!-- badges: end -->

The goal of datautils is to make miscellaneous data processing tasks
easier.

## Installation

You can install datautils from [GitHub](https://www.github.com) with:

``` r
if(!require("devtools", quietly = TRUE)) install.packages('devtools')
devtools::install_github("MiguelRodo/datautils.git")
```

## Examples

Load the package.

``` r
library(datautils)
```

Display a random selection of (a limited number) of unique entries from
each column.

``` r
data('mtcars')
view_cols(mtcars)
#> [1] "mpg"
#> [1] 32.4 33.9 19.7 21.4 15.8
#> [1] "_____________________"
#> [1] "cyl"
#> [1] 4 8 6
#> [1] "_____________________"
#> [1] "disp"
#> [1] 167.6  78.7 350.0 140.8 120.1
#> [1] "_____________________"
#> [1] "hp"
#> [1]  95 180  93  91 110
#> [1] "_____________________"
#> [1] "drat"
#> [1] 3.15 4.43 4.93 3.77 3.73
#> [1] "_____________________"
#> [1] "wt"
#> [1] 2.140 1.835 1.935 2.320 3.440
#> [1] "_____________________"
#> [1] "qsec"
#> [1] 16.46 17.05 17.98 14.60 20.22
#> [1] "_____________________"
#> [1] "vs"
#> [1] 1 0
#> [1] "_____________________"
#> [1] "am"
#> [1] 0 1
#> [1] "_____________________"
#> [1] "gear"
#> [1] 5 4 3
#> [1] "_____________________"
#> [1] "carb"
#> [1] 3 6 4 2 1
#> [1] "_____________________"
```

Correct error where Excel reads in incorrectly due to differences in the
decimal symbol between systems. At present only fixes error where
original data uses a comma and system being read into uses a full stop.

``` r
# vector of data (as if from Excel)
x <- c("1,32", "1", "0,23", "3,23E-2", NA)
x_corrected <- convert_character_to_number_correctly(x = x)
# original data alongside corrected data
tibble::tibble(original = x, corrected = x_corrected)
#> # A tibble: 5 x 2
#>   original corrected
#>   <chr>        <dbl>
#> 1 1,32        1.32  
#> 2 1           1     
#> 3 0,23        0.23  
#> 4 3,23E-2     0.0323
#> 5 <NA>       NA
```

Display a subset of entries per group (a thin wrapper around
`dplyr::group_by` and `dplyr::slice`).

``` r
data('cars')
cars[,'grp'] <- rep(letters[1:5], each = 10)
view_slice(cars, group = 'grp', n_slice = 2)
#> # A tibble: 10 x 3
#> # Groups:   grp [5]
#>    speed  dist grp  
#>    <dbl> <dbl> <chr>
#>  1     4     2 a    
#>  2     4    10 a    
#>  3    11    28 b    
#>  4    12    14 b    
#>  5    14    36 c    
#>  6    14    60 c    
#>  7    17    50 d    
#>  8    18    42 d    
#>  9    20    52 e    
#> 10    20    56 e
```
