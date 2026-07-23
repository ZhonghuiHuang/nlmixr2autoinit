# Create full control list for initial parameter estimation

Aggregates modular control functions into a structured list for use in
population pharmacokinetic parameter initialization.

## Usage

``` r
initsControl(
  ss.control = ss_control(),
  pooled.control = pooled_control(),
  nca.control = nca_control(),
  fallback.control = fallback_control(),
  selmetrics = "rRMSE2",
  hybrid.base = TRUE,
  preferNCA = TRUE
)
```

## Arguments

- ss.control:

  A control list consistent with the structure returned by ss_control().

- pooled.control:

  A control list consistent with the structure returned by
  pooled_control().

- nca.control:

  A control list consistent with the structure returned by
  nca_control().

- fallback.control:

  A control list consistent with the structure returned by
  fallback_control().

- selmetrics:

  A character string or vector specifying model performance metrics to
  evaluate. Must be one or more of "APE", "MAE", "MAPE", "RMSE",
  "rRMSE1", or "rRMSE2". Default is "rRMSE2".

- hybrid.base:

  Logical. If TRUE, enables hybrid evaluation mode in which model
  performance is assessed using mixed parameter combinations across
  methods. If FALSE, each method is evaluated independently. Default is
  TRUE.

- preferNCA:

  Logical. If TRUE and selmetrics equals "rRMSE2", the lowest rRMSE2 is
  selected first. If the best-performing method is not NCA-based, the
  function then checks whether an NCA-based method offers a lower
  rRMSE1. If so, the NCA method is selected. Default is TRUE.

## Value

A named list combining all control modules for parameter estimation.

## See also

[ss_control](https://init.nlmixr2auto.org/reference/ss_control.md),
[pooled_control](https://init.nlmixr2auto.org/reference/pooled_control.md),
[nca_control](https://init.nlmixr2auto.org/reference/nca_control.md),
[fallback_control](https://init.nlmixr2auto.org/reference/fallback_control.md)

## Examples

``` r
initsControl(
  pooled.control = pooled_control(nbins = 8),
  fallback.control = fallback_control(
    sigma_method_additive = "fixed_fraction"
  )
)
```
