# Performs non-compartmental analysis on pooled data

Implements pooled concentration–time profiling followed by
non-compartmental analysis (NCA) to derive pharmacokinetic parameters
across single-dose, multiple-dose, or combined dosing scenarios under
bolus, oral, or infusion routes.

## Usage

``` r
run_pooled_nca(
  dat,
  route = c("bolus", "oral", "infusion"),
  dose_type = c("first_dose", "repeated_doses", "combined_doses"),
  pooled = NULL,
  pooled_ctrl = pooled_control(),
  nca_ctrl = nca_control()
)
```

## Arguments

- dat:

  A data frame containing raw time–concentration data in the standard
  nlmixr2 format.

- route:

  Route of administration. Must be one of bolus, oral, or infusion.

- dose_type:

  Classified as first_dose, repeated_doses, or combined_doses based on
  whether observed concentrations occur following the first
  administration, during repeated dosing, or across both contexts.

- pooled:

  Optional pre-pooled data returned by `get_pooled_data`.

- pooled_ctrl:

  Optional list of control parameters used by
  [`get_pooled_data()`](https://init.nlmixr2auto.org/reference/get_pooled_data.md)
  for pooling observations. Defaults to output from
  [`pooled_control()`](https://init.nlmixr2auto.org/reference/pooled_control.md).

- nca_ctrl:

  List of options created by `nca_control` for NCA settings.

## Value

A list containing NCA results according to the selected dose_type.

## Details

The function first pools individual subject data into representative
concentration–time profiles using `get_pooled_data` based on the
settings in `pooled_ctrl`. The pooled profiles are then passed to
`getnca`, which computes non-compartmental parameters using rules
specified in `nca_ctrl`.

## See also

[`get_pooled_data`](https://init.nlmixr2auto.org/reference/get_pooled_data.md),
[`bin.time`](https://init.nlmixr2auto.org/reference/bin.time.md),
[`getnca`](https://init.nlmixr2auto.org/reference/getnca.md)

## Author

Zhonghui Huang

## Examples

``` r
out   <- processData(Bolus_1CPT)
dat   <- out$dat
route <- out$Datainfo$Value[out$Datainfo$Infometrics == "Dose Route"]

run_pooled_nca(
  dat       = dat,
  dose_type = "first_dose",
  route     = route
)$nca.fd.results
```
