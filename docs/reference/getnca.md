# Perform non-compartmental pharmacokinetic analysis

Calculates key pharmacokinetic parameters using non-compartmental
methods for both intravenous and oral administration data.

## Usage

``` r
getnca(
  x,
  y,
  dose = 1,
  trapezoidal.rule = c("linear_up_log_down", "linear"),
  ss = 0,
  duration = NULL,
  nlastpoints = 3,
  slope.method = c("bestfitforce", "bestfit"),
  route = c("bolus", "oral", "infusion")
)
```

## Arguments

- x:

  Numeric vector of observation times.

- y:

  Numeric vector of drug concentration measurements.

- dose:

  Administered dose (default = 1).

- trapezoidal.rule:

  Method for AUC calculation:

  - `"linear"` - Linear trapezoidal method (default)

  - `"linear_up_log_down"` - Linear-up/log-down method (linear for
    ascending concentrations, logarithmic for descending)

- ss:

  Steady-state flag:

  - 0 - Use extrapolated \\AUC\_{0 \rightarrow \infty}\\ for clearance
    (default)

  - 1 - Use observed \\AUC\_{0 \rightarrow \mathrm{last}}\\ for
    clearance

- duration:

  Infusion duration (required if `route = "infusion"`).

- nlastpoints:

  Number of terminal points for slope estimation (default = 3).

- slope.method:

  Method for estimating terminal slope (\\\lambda_z\\):

  - `"bestfitforce"` - Force estimation using decreasing number of
    terminal points if best-fit fails (default)

  - `"bestfit"` - Use automated best-fit selection based on adjusted
    R-squared

- route:

  Administration route:

  - `"bolus"` - Intravenous bolus (default)

  - `"oral"` - Oral administration

  - `"infusion"` - Intravenous infusion

## Value

A list containing:

- cl - Clearance (CL), calculated as Dose/AUC

- vz - volume of distribution (Vz), calculated as CL / lambdaz

- half_life - Terminal elimination half-life, computed as ln(2) /
  lambdaz

- auct - Area under the concentration–time curve from time 0 to last
  measurable concentration

- auc0_inf - AUC extrapolated to infinity

- C_last - Last non-zero measurable concentration

- lambdaz - Terminal elimination rate constant

- aumc_0_t - Area under the first moment curve from time 0 to last
  measurable concentration

- aumc_0_inf - AUMC extrapolated to infinity

- used_points - Number of time–concentration points used to estimate
  lambdaz

- adj.r.squared - Adjusted R-squared of the terminal phase regression

- messages - Warning or diagnostic messages returned during the
  calculation

## Examples

``` r
# IV bolus example
dat <- data.frame(TIME = c(0.5, 1, 2, 4, 6, 8),
                  DV = c(12, 8, 5, 3, 2, 1))
getnca(x = dat$TIME, y = dat$DV, dose = 1)

# IV infusion example
dat <- data.frame(TIME = c(0.5, 1, 2, 4, 6, 8),
                  DV = c(2, 8, 5, 3, 2, 1))
getnca(x = dat$TIME, y = dat$DV, dose = 1, route = "infusion", duration = 1)

# Oral administration example
dat <- data.frame(TIME = c(0, 1, 2, 4, 6, 8),
                  DV = c(0, 9, 12, 8, 6, 2))
getnca(x = dat$TIME, y = dat$DV, route = "oral")
```
