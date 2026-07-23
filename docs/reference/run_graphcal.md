# Run graphical analysis of pharmacokinetic parameters

Performs graphical estimation of pharmacokinetic parameters based on
pooled concentration–time data and the specified route of
administration.

## Usage

``` r
run_graphcal(
  dat,
  route,
  dose_type = c("first_dose", "repeated_doses", "combined_doses"),
  pooled = NULL,
  pooled_ctrl = pooled_control(),
  ...
)
```

## Arguments

- dat:

  A data frame containing raw time–concentration data in the standard
  nlmixr2 format.

- route:

  Route of administration. Must be one of bolus, oral, or infusion.

- dose_type:

  Specifies the dosing context of the pharmacokinetic observations.
  Classified as first_dose, repeated_doses, or combined_doses based on
  whether observed concentrations occur following the first
  administration, during repeated dosing, or across both contexts.

- pooled:

  Optional pooled dataset. If NULL, pooling is performed internally.

- pooled_ctrl:

  Control settings created by
  [`pooled_control()`](https://init.nlmixr2auto.org/reference/pooled_control.md)
  for time binning and pooling.

- ...:

  Additional arguments passed to graphical calculation functions.

## Value

A list containing graphical estimates of key pharmacokinetic parameters.

## Details

The function pools individual profiles using
[`get_pooled_data()`](https://init.nlmixr2auto.org/reference/get_pooled_data.md)
when needed, and then applies route-specific graphical methods
(`graphcal_iv` or `graphcal_oral`) to estimate parameters such as
clearance, volume of distribution, terminal slope, and absorption rate
constant (for oral data).

## See also

[`graphcal_iv`](https://init.nlmixr2auto.org/reference/graphcal_iv.md),
[`graphcal_oral`](https://init.nlmixr2auto.org/reference/graphcal_oral.md),
[`get_pooled_data`](https://init.nlmixr2auto.org/reference/get_pooled_data.md)

## Author

Zhonghui Huang

## Examples

``` r
# Example 1 (iv case)
dat <- Bolus_1CPT
dat <- processData(dat)$dat
run_graphcal(dat, route="bolus")

# Example 2 (oral case)
dat <- Oral_1CPT
dat <- processData(dat)$dat
run_graphcal(dat, route="oral")

# Example 3 (infusion case).
# Approximate calculation. only use when the infusion duration is very short

dat <- Infusion_1CPT
dat <- processData(dat)$dat
run_graphcal(dat, route="infusion")
```
