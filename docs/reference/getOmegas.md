# Generate ETA variance and covariance table

This function constructs a combined table containing:

- **ETA variances** (e.g., `eta.cl`, `eta.vc`), which represent
  inter-individual variability (IIV) in pharmacokinetic parameters;

- **Derived covariances** (e.g., `cov.eta_cl_vc`) computed from ETA
  variances and assumed pairwise correlations.

## Usage

``` r
getOmegas()
```

## Value

A `data.frame` with columns: `Parameters`, `Methods`, and `Values`.

## Details

ETA variances are initialized to 0.1 by default. Correlations within
defined omega blocks (block 1: `eta.vmax`, `eta.km`; block 2: `eta.cl`,
`eta.vc`, `eta.vp`, `eta.vp2`, `eta.q`, `eta.q2`) are assumed to be 0.1
and used to compute covariances as: \$\$Cov(i, j) = sqrt(Var_i) \*
sqrt(Var_j) \* Corr(i, j)\$\$

The resulting output format aligns with `Recommended_initial_estimates`.

## Examples

``` r
getOmegas()
```
