# Mark dose number

Assigns sequential dose numbers based on dosing events (EVID) within
each subject.

## Usage

``` r
mark_dose_number(dat)
```

## Arguments

- dat:

  A data frame containing raw time–concentration data in the standard
  nlmixr2 format.

## Value

A modified data frame with an added column named dose_number, indicating
the sequential dose count within each subject and reset group.

## Author

Zhonghui Huang

## Examples

``` r
mark_dose_number(Bolus_1CPT)
mark_dose_number(Infusion_1CPT)
mark_dose_number(Oral_1CPT)
```
