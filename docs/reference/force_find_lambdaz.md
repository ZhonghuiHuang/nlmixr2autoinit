# Forceful estimation of terminal slope

Estimates the terminal elimination rate constant (lambda_z) of a
pharmacokinetic profile. The function first attempts to use the
`find_best_lambdaz` method. If no valid estimate is obtained, it falls
back to a simplified log-linear regression using progressively fewer
data points to enforce a negative slope.

## Usage

``` r
force_find_lambdaz(time, conc, ...)
```

## Arguments

- time:

  Numeric vector of time points.

- conc:

  Numeric vector of concentration values corresponding to time.

- ...:

  Additional arguments passed to find_best_lambdaz (e.g., nlastpoints).

## Value

A list containing:

- lambdaz: Estimated terminal elimination rate constant (1/time)

- intercept: Intercept of the log-linear regression, used to extrapolate
  concentration at time zero

- method: Method used (`find_best_lambdaz` or fallback regression)

- UsedPoints: Number of time-concentration points used for estimation

- adj.r.squared: Adjusted R-squared (available only when using
  `find_best_lambdaz`)

- message: Diagnostic message summarizing the outcome

- slopefit: Fitted linear model object

## Details

This function implements a two-step strategy to ensure estimation of the
terminal elimination slope:

- First, it applies `find_best_lambdaz` to automatically select the best
  fitting terminal phase segment based on adjusted R-squared
  optimization.

- If `find_best_lambdaz` fails (e.g., limited data), the function
  forcibly fits simplified linear models using progressively fewer
  points (starting from n-1 down to 2) until a negative slope is
  identified. In fallback mode, adjusted R-squared is not considered.

## See also

[find_best_lambdaz](https://init.nlmixr2auto.org/reference/find_best_lambdaz.md)

## Author

Zhonghui Huang

## Examples

``` r
time <- c(0.5, 1, 2, 4, 6, 8, 10)
conc <- c(12, 8, 5, 3, 2, 1.5, 1)
force_find_lambdaz(time, conc)
```
