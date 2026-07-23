# Print method for `getPPKinits` objects

Prints a summary of the results from the initial parameter estimation
pipeline, including recommended initial estimates, ETA variance
estimates, and parameter descriptions. It is the default S3 `print`
method for objects of class `getPPKinits`.

## Usage

``` r
# S3 method for class 'getPPKinits'
print(x, ...)
```

## Arguments

- x:

  An object of class `getPPKinits` containing the initial parameter
  estimation results. Expected components include:

  - `Recommended_initial_estimates`: A data frame with estimated values
    and selection methods.

  - `Parameter.descriptions`: A character vector explaining the meaning
    of each parameter.

  - `time.spent`: Time taken to compute the estimates.

- ...:

  Additional arguments (for compatibility with the generic
  [`print()`](https://rdrr.io/r/base/print.html)).

## Value

Prints a formatted summary to the console.

## Examples

``` r
# \donttest{
## Oral example
inits.out <- getPPKinits(Bolus_1CPT)
print(inits.out)
# }
```
