# Fit intravenous pharmacokinetic data to a one-compartment linear elimination model

Fits intravenous (IV) pharmacokinetic data to a one-compartment model
with first-order elimination using the naive pooled data approach.
Supports multiple estimation methods provided by nlmixr2 and can
optionally return only predicted concentrations to support efficient
simulation workflows.

## Usage

``` r
Fit_1cmpt_iv(
  data,
  est.method,
  input.cl,
  input.vd,
  input.add,
  ncores = 2,
  return.pred.only = FALSE,
  ...
)
```

## Arguments

- data:

  A data frame of IV pharmacokinetic data formatted for nlmixr2.

- est.method:

  Estimation method to use in nlmixr2. Must be one of: `"rxSolve"`,
  `"nls"`, `"nlm"`, `"nlminb"`, or `"focei"`.

- input.cl:

  Initial estimate of clearance (CL).

- input.vd:

  Initial estimate of volume of distribution (V).

- input.add:

  Initial estimate of the additive residual error.

- ncores:

  Number of cores to use for parallelization, passed to `rxControl()`.
  Default is 2.

- return.pred.only:

  Logical; if `TRUE`, returns a data frame with only predicted
  concentrations (`cp`) for all observations in the input data.

- ...:

  Additional arguments passed to `nlmixr2()`, such as a user-defined
  `control = foceiControl(...)` or other control settings.

## Value

If `return.pred.only = TRUE`, returns a `data.frame` with a single
column `cp` (predicted concentrations). Otherwise, returns a fitted
model object produced by nlmixr2.

## Author

Zhonghui Huang

## Examples

``` r
 # \donttest{
dat <- Bolus_1CPT
# Run simulation
Fit_1cmpt_iv(
  data = dat,
  est.method = "rxSolve",
  input.cl = 4,
  input.vd = 70,
  input.add = 1
)
# Return only predicted concentrations
Fit_1cmpt_iv(
 data = dat,
 est.method = "rxSolve",
 input.cl = 4,
 input.vd = 70,
 input.add = 0,
 return.pred.only = TRUE
)
# }
```
