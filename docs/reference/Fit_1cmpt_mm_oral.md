# Fit oral pharmacokinetic data to a one-compartment model with Michaelis-Menten elimination

Fits oral pharmacokinetic data to a one-compartment model with
first-order absorption and Michaelis-Menten (nonlinear) elimination
using the naive pooled data approach. Supports multiple estimation
methods available in nlmixr2, and optionally returns only predicted
concentrations to reduce memory use in simulation workflows.

## Usage

``` r
Fit_1cmpt_mm_oral(
  data,
  est.method,
  input.ka,
  input.vmax,
  input.km,
  input.vd,
  input.add,
  ncores = 2,
  return.pred.only = FALSE,
  ...
)
```

## Arguments

- data:

  A data frame of oral pharmacokinetic data formatted for nlmixr2.

- est.method:

  Estimation method to use in nlmixr2, one of: `"rxSolve"`, `"nls"`,
  `"nlm"`, `"nlminb"`, or `"focei"`.

- input.ka:

  Initial estimate of the absorption rate constant (ka).

- input.vmax:

  Initial estimate of the maximum elimination rate (Vmax).

- input.km:

  Initial estimate of the Michaelis constant (Km).

- input.vd:

  Initial estimate of the volume of distribution (V).

- input.add:

  Initial estimate of the additive residual error.

- ncores:

  Number of cores to use for parallelization, passed to `rxControl()`.
  Default is 2.

- return.pred.only:

  Logical; if `TRUE`, returns a data frame with only predicted
  concentrations (`cp`) for all observations in the input data.

- ...:

  Optional arguments passed to `nlmixr2()`, such as a custom
  `control = foceiControl(...)` or other control objects.

## Value

If `return.pred.only = TRUE`, returns a `data.frame` with columns `cp`
(predicted concentration) and `DV` (observed data). Otherwise, returns a
fitted model object produced by nlmixr2.

## Author

Zhonghui Huang

## Examples

``` r
 # \donttest{
dat <- Oral_1CPTMM
# Run simulation
Fit_1cmpt_mm_oral(
  data = dat,
  est.method = "rxSolve",
  input.ka = 1,
  input.vmax = 1000,
  input.km = 250,
  input.vd = 70,
  input.add = 10
)
# Return only predicted concentrations
Fit_1cmpt_mm_oral(
  data = dat,
  est.method = "rxSolve",
  input.ka = 1,
  input.vmax = 1000,
  input.km = 250,
  input.vd = 70,
  input.add = 10
)
# }
```
