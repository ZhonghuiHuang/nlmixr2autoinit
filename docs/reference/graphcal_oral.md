# Graphical calculation of pharmacokinetic parameters for oral administration

Estimates key pharmacokinetic parameters from oral concentration–time
data using graphical methods, including absorption rate constant (ka),
elimination rate constant (kel), terminal slope, extrapolated
concentration (C0exp), apparent volume of distribution (Vd/F), and
clearance (Cl/F).

## Usage

``` r
graphcal_oral(dat, dose = 1, ...)
```

## Arguments

- dat:

  A data frame containing TIME (time after dosing) and DV (observed
  concentration).

- dose:

  Administered dose amount. Defaults to 1.

- ...:

  Additional arguments passed to
  [`find_best_lambdaz()`](https://init.nlmixr2auto.org/reference/find_best_lambdaz.md).

## Value

A list containing graphical estimates of ka, kel, lambda_z, C0exp, Vd/F,
and Cl/F.

## Details

The terminal slope (lambdaz) is estimated using
[`force_find_lambdaz()`](https://init.nlmixr2auto.org/reference/force_find_lambdaz.md).
The apparent volume of distribution and clearance are computed using the
following relationships: \$\$Vd/F = \frac{Dose \times ka}{C_0 \times
(ka - kel)}\$\$ \$\$Cl/F = kel \times Vd/F\$\$ where `ka` is estimated
from the absorption phase.

## See also

[`find_best_lambdaz`](https://init.nlmixr2auto.org/reference/find_best_lambdaz.md)

## Author

Zhonghui Huang

## Examples

``` r
dat <- data.frame(TIME = c(0.5, 1, 2, 4, 6, 8, 10),
                  DV = c(1, 2, 5, 3, 2, 1.5, 1))
graphcal_oral(dat, dose = 100, route = "oral")
```
