# Calculate time after dose for pharmacokinetic data

Calculate time after dose (TAD) for pharmacokinetic observations.

## Usage

``` r
calculate_tad(dat, verbose = FALSE)
```

## Arguments

- dat:

  A data frame containing raw time–concentration data in the standard
  nlmixr2 format.

- verbose:

  Logical; if TRUE, prints informational messages during processing
  (e.g., when generating dose numbers). Default is FALSE.

## Value

A modified data frame with added columns:

- tad: time after dose, calculated as the observation time minus the
  time of the most recent prior dose; set to NA for dosing records

- iiobs: interdose interval inherited from the most recent dosing record

- rateobs: infusion rate inherited from the most recent dosing record

- routeobs (optional): route of administration inherited from the most
  recent dosing record, included only if route information is present

- dose_number: sequential dose number, generated if not already present

## Details

The procedure identifies dosing events based on the event identifier
(EVID) and assigns each observation the attributes of the most recent
prior dose. The time after dose is then calculated for observation rows.
If `dose_number` column is not present in the input, it is automatically
created for each subject.

## Author

Zhonghui Huang

## Examples

``` r
calculate_tad(Bolus_1CPT)
calculate_tad(Infusion_1CPT)
calculate_tad(Oral_1CPT)
```
