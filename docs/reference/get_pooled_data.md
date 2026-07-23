# Generate pooled data for pharmacokinetic analysis

Processes pharmacokinetic data and produces pooled datasets according to
the dosing context. Data can be grouped based on first dose, repeated
dosing, or a combination of both, with control over binning and time
alignment.

## Usage

``` r
get_pooled_data(
  dat,
  dose_type = c("first_dose", "repeated_doses", "combined_doses"),
  pooled_ctrl = pooled_control()
)
```

## Arguments

- dat:

  A data frame containing raw time–concentration data in the standard
  nlmixr2 format.

- dose_type:

  Specifies the dosing context of the pharmacokinetic observations.
  Classified as:

  - first_dose: data include only observations following the initial
    administration

  - repeated_doses: data include only observations during repeated or
    steady-state dosing

  - combined_doses: data include observations from both first-dose and
    repeated-dose intervals

- pooled_ctrl:

  A list of control parameters created by 'pooled_control', including
  settings for binning and time rounding.

## Value

A list containing pooled pharmacokinetic datasets depending on the
specified dose type:

- datpooled_fd: pooled data for first-dose observations

- datpooled_efd: pooled data for repeated dosing

- datpooled_all: pooled data combining first-dose and repeated-dose
  observations

## Details

For repeated-doses and combined-doses classifications, the most common
interdose interval is identified from dosing records and used to
determine whether observations fall within the relevant interval. If
tad_rounding is TRUE, both time after dose and dosing interval are
rounded before comparison.

## See also

[pooled_control](https://init.nlmixr2auto.org/reference/pooled_control.md),
[trimmed_geom_mean](https://init.nlmixr2auto.org/reference/trimmed_geom_mean.md)

## Author

Zhonghui Huang

## Examples

``` r
dat <- processData(Bolus_1CPT)$dat
get_pooled_data(dat, dose_type = "combined_doses")
```
