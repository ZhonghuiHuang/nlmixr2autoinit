# Graphical calculation of clearance and volume of distribution (IV route)

Estimates clearance (CL), volume of distribution (Vd), terminal slope
(lambdaz), and extrapolated concentration at time zero (C0exp) from
intravenous pharmacokinetic data using graphical methods.

## Usage

``` r
graphcal_iv(dat, dose = 1, ...)
```

## Arguments

- dat:

  A data frame containing TIME (time after dosing) and DV (observed
  concentration).

- dose:

  Administered dose amount. Defaults to 1.

- ...:

  Additional arguments passed to
  [`force_find_lambdaz()`](https://init.nlmixr2auto.org/reference/force_find_lambdaz.md).

## Value

A list containing graphical estimates of CL, Vd, lambda_z, and C0exp.

## Details

Terminal slope (lambdaz) is estimated using
[`force_find_lambdaz()`](https://init.nlmixr2auto.org/reference/force_find_lambdaz.md),
which applies an automated phase selection strategy with fallback
regression when required.

## See also

[`force_find_lambdaz`](https://init.nlmixr2auto.org/reference/force_find_lambdaz.md)

## Author

Zhonghui Huang

## Examples

``` r
dat <- data.frame(TIME = c(0.5, 1, 2, 4, 6, 8, 10),
                  DV = c(12, 8, 5, 3, 2, 1.5, 1))
graphcal_iv(dat, dose = 100)
```
