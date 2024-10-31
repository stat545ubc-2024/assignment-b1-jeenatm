assignment b-1
================
Jeenat Mehareen
2024-10-31

``` r
suppressPackageStartupMessages(library(devtools)) # for devtools package
suppressPackageStartupMessages(library(dplyr)) # for data manipulation
suppressPackageStartupMessages(library(testthat)) # for testing functions
suppressPackageStartupMessages(library(digest)) #digests outputs for testing 
suppressPackageStartupMessages(library(palmerpenguins)) # for testing a sample tibble
```

**Exercise 1 and 2: Making and documenting my function**

``` r
#' Convert Millimeters to Inches
#'
#' This function converts measurements from millimeters (mm) to inches: 1 inch = 25.4 mm.
#' It is designed to ignore non-numeric inputs.
#' It will accept a numeric vector as input and return vector of converted values
#' 
#' 
#' @param mm A numeric vector, measurements are in millimeters, hence the name mm. Non-numeric values will result in an error.
#' @return A numeric vector, it will convert mm to inches. If input values are NA it will return "NA"
#' @export
#'
#' @examples Showing some example for usage of single value, vectors, and NA 
#' mm_to_in(25.4) # Should return 1
#' mm_to_in(c(25.4, 127)) # Should return 1 and 5
#' mm_to_in(NA) # Should return NA


mm_to_in <- function(mm) {
  # Check if the input is numeric; throw an error if not
  if (!is.numeric(mm)) {
    stop("Input must be a numeric vector, measurements must be in mm")
  }
  
  # otherwise convert the value
  inch <- mm / 25.4
  return(inch)
}
```

**Exercise 3: Examples**

<p>
The following demonstrates an example of unit conversion using manual input
of 200mm
<p>

``` r
mm_to_in(200)
```

    ## [1] 7.874016

<p>
This shows an example using a unit conversion on a column in a dataframe
(using penguins and flipper_length_mm)
<p>

``` r
a <- penguins %>%
  mutate(mm_to_in(flipper_length_mm))
a
```

    ## # A tibble: 344 × 9
    ##    species island    bill_length_mm bill_depth_mm flipper_length_mm body_mass_g
    ##    <fct>   <fct>              <dbl>         <dbl>             <int>       <int>
    ##  1 Adelie  Torgersen           39.1          18.7               181        3750
    ##  2 Adelie  Torgersen           39.5          17.4               186        3800
    ##  3 Adelie  Torgersen           40.3          18                 195        3250
    ##  4 Adelie  Torgersen           NA            NA                  NA          NA
    ##  5 Adelie  Torgersen           36.7          19.3               193        3450
    ##  6 Adelie  Torgersen           39.3          20.6               190        3650
    ##  7 Adelie  Torgersen           38.9          17.8               181        3625
    ##  8 Adelie  Torgersen           39.2          19.6               195        4675
    ##  9 Adelie  Torgersen           34.1          18.1               193        3475
    ## 10 Adelie  Torgersen           42            20.2               190        4250
    ## # ℹ 334 more rows
    ## # ℹ 3 more variables: sex <fct>, year <int>,
    ## #   `mm_to_in(flipper_length_mm)` <dbl>

<p>
This shows error when trying to convert string values with the function
<p>
<p>
This shows an error with the message “Input must be a numeric vector,
measurements must be in mm” when trying to convert string values with
the function:
</p>

``` r
# Attempting to convert non-numeric input should result in an error
mm_to_in("fail") # This will trigger an error since the input is not numeric
```

    ## Error in mm_to_in("fail"): Input must be a numeric vector, measurements must be in mm

**Exercise 4: Testing the function**

``` r
##Test 1
test_that("Testing mm_to_in function",{
   expect_equal(mm_to_in(124), 124 / 25.4)
             
})
```

    ## Test passed 🎊

``` r
##Test 2
test_that("Testing mm_to_in function",{
expect_equal(mm_to_in(c(25.4, NA)), c(25.4 / 25.4, NA))
})
```

    ## Test passed 🥳

``` r
##Test 3
test_that("Testing mm_to_in function",{
  expect_error(mm_to_in("stat"), "Input must be a numeric vector")
})
```

    ## Test passed 🥳
