# Fit intravenous pharmacokinetic data to a three-compartment linear elimination model

Fits intravenous (IV) pharmacokinetic data to a three-compartment model
with linear (first-order) elimination using the naive pooled data
approach. Supports multiple estimation methods provided by nlmixr2 and
can optionally return only predicted concentrations to support efficient
simulation workflows.

## Usage

``` r
Fit_3cmpt_iv(
  data,
  est.method,
  input.cl,
  input.vc3cmpt,
  input.vp3cmpt,
  input.vp23cmpt,
  input.q3cmpt,
  input.q23cmpt,
  input.add,
  ncores = 2,
  return.pred.only = FALSE,
  ...
)
```

## Arguments

- data:

  A data frame containing IV pharmacokinetic data formatted for nlmixr2.

- est.method:

  Estimation method to use in nlmixr2. Must be one of: `"rxSolve"`,
  `"nls"`, `"nlm"`, `"nlminb"`, or `"focei"`.

- input.cl:

  Initial estimate of clearance (CL).

- input.vc3cmpt:

  Initial estimate of central volume of distribution (V1).

- input.vp3cmpt:

  Initial estimate of first peripheral volume of distribution (V2).

- input.vp23cmpt:

  Initial estimate of second peripheral volume of distribution (V3).

- input.q3cmpt:

  Initial estimate of first inter-compartmental clearance (Q1).

- input.q23cmpt:

  Initial estimate of second inter-compartmental clearance (Q2).

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
dat <- Bolus_2CPT
# Run simulation
Fit_3cmpt_iv(
  data = dat,
  est.method = "rxSolve",
  input.cl = 4,
  input.vc3cmpt = 70,
  input.vp3cmpt = 35,
  input.vp23cmpt = 5,
  input.q3cmpt = 4,
  input.q23cmpt = 4,
  input.add = 10
)
# Return only predicted concentrations
Fit_3cmpt_iv(
  data = dat,
  est.method = "rxSolve",
  input.cl = 4,
  input.vc3cmpt = 70,
  input.vp3cmpt = 35,
  input.vp23cmpt = 35,
  input.q3cmpt = 4,
  input.q23cmpt = 4,
  input.add = 10,
  return.pred.only = TRUE
)
# }
```
