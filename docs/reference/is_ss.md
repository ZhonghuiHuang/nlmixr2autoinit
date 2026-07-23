# Determine steady state for pharmacokinetic observations

Evaluates whether pharmacokinetic observations have reached steady state
based on user-defined control settings. The classification can be based
on a fixed number of doses, the number of half-lives relative to the
dosing interval, or a combination of both criteria.

## Usage

``` r
is_ss(df, ssctrl = ss_control(), half_life = NA)
```

## Arguments

- df:

  A data frame containing pharmacokinetic data. It should include
  columns for ID, EVID, SSflag, TIME, AMT, and tad.

- ssctrl:

  A control list consistent with the structure returned by ss_control().
  It specifies the method and thresholds for steady-state evaluation.

- half_life:

  Numeric value representing the drug half-life. Required when the
  method in ss_control() is based on half-life or uses a combined
  approach.

## Value

A data frame with added columns indicating steady-state status, the
dosing interval for steady-state observations, and the method used to
classify steady state.

## Details

The function determines steady state by examining each observation in
relation to prior dosing history. The required number of doses is
calculated based on the specified method in ss_control(). Observation
times are evaluated to confirm that dose interval and dose amount
variability fall within acceptable limits and that the time after dose
is within the most recent dosing interval. Observations manually marked
as steady state using SSflag are also recognized as steady state.

## See also

ss_control()

## Examples

``` r
dat <- pheno_sd
dat <- processData(dat)$dat
out <- is_ss(df = dat)
out[out$SteadyState == TRUE & !is.na(out$SteadyState),
    c("ID", "TIME", "DV", "EVID", "SteadyState")]
```
