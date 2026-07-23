# Compute overall residual variability from elimination phase

Applies `getsigmas` to each individual and dose group after filtering
observation records (EVID == 0), and calculates trimmed mean estimates
of additive and proportional residual variability.

## Usage

``` r
getsigma(df, nlastpoints = 3, sigma_trim = 0.05)
```

## Arguments

- df:

  Full pharmacokinetic dataset containing at least the columns: EVID,
  ID, TIME, DV, and routeobs.

- nlastpoints:

  Number of terminal points used for elimination phase regression in
  each group (passed to getsigmas).

- sigma_trim:

  Trimming proportion used when calculating trimmed means of residual
  standard deviations. Default is 0.05.

## Value

A list containing:

- summary: Named list with trimmed mean values of additive and
  proportional residual variability

- full: Data frame with residual estimates for each individual-dose
  group

## Details

The function groups the dataset by subject and dose occasion, applies
elimination-phase residual analysis using `getsigmas`, and summarizes
the individual residual standard deviations by their trimmed means. This
provides population-level estimates of additive and proportional
residual unexplained variability (RUV).

## See also

[getsigmas](https://init.nlmixr2auto.org/reference/getsigmas.md)

## Author

Zhonghui Huang

## Examples

``` r
dat <- Bolus_1CPT
dat <- processData(dat)$dat
getsigma(dat)
```
