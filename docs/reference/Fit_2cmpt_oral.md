# Fit oral pharmacokinetic data to a two-compartment model

Fits oral pharmacokinetic data to a two-compartment model with
first-order absorption and first-order elimination using the naive
pooled data approach. Supports multiple estimation methods available in
nlmixr2, and optionally returns only predicted concentrations to support
simulation workflows.

## Usage

``` r
Fit_2cmpt_oral(
  data,
  est.method,
  input.ka,
  input.cl,
  input.vc2cmpt,
  input.vp2cmpt,
  input.q2cmpt,
  input.add,
  ncores = 2,
  return.pred.only = FALSE,
  ...
)
```

## Arguments

- data:

  A data frame containing oral pharmacokinetic data formatted for
  nlmixr2,

- est.method:

  Estimation method to use in nlmixr2, one of: `"rxSolve"`, `"nls"`,
  `"nlm"`, `"nlminb"`, or `"focei"`.

- input.ka:

  Initial estimate of the absorption rate constant (ka).

- input.cl:

  Initial estimate of clearance (CL).

- input.vc2cmpt:

  Initial estimate of central volume of distribution (V1).

- input.vp2cmpt:

  Initial estimate of peripheral volume of distribution (V2).

- input.q2cmpt:

  Initial estimate of inter-compartmental clearance (Q).

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
dat <- Oral_2CPT[Oral_2CPT$ID<11,]
# Run simulation
Fit_2cmpt_oral(
  data = dat,
  est.method = "rxSolve",
  input.ka = 1,
  input.cl = 4,
  input.vc2cmpt = 70,
  input.vp2cmpt = 40,
  input.q2cmpt = 10,
  input.add = 10
)
# }
```
