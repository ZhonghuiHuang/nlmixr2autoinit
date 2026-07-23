# Calculate the absorption rate constant using the Wagner-Nelson method

Calculates absorption rate constant using the Wagner–Nelson method for
single-dose extravascular pharmacokinetics.

## Usage

``` r
ka_wanger_nelson(dat, nca.out = NULL)
```

## Arguments

- dat:

  A data frame containing two columns: 'TIME' for sampling time points
  and 'DV' for observed plasma drug concentrations.

- nca.out:

  Optional object containing results from a previous noncompartmental
  analysis. It must include 'auc0_inf' for the area under the
  concentration-time curve extrapolated to infinity and 'lambdaz' for
  the terminal elimination rate constant. If not provided, the function
  calls 'getnca' internally using the input data.

## Value

A list containing:

- ka: Estimated absorption rate constant

- dat_out_wanger_nelson: Input data frame augmented with calculated
  pharmacokinetic variables including cumulative AUC, fraction absorbed,
  and fraction remaining

## Details

The Wagner-Nelson method estimates the fraction of drug absorbed over
time based on the principle of mass balance, where the unabsorbed
fraction is quantified as the proportion of the administered dose that
has not yet entered systemic circulation. A linear regression is applied
to the natural logarithm of the unabsorbed fraction versus time, and the
negative slope of this regression corresponds to the first-order
absorption rate constant 'ka'.

Key assumptions:

- Single-dose oral or extravascular administration

- First-order absorption and first-order elimination

- Linear pharmacokinetics with 'ka' greater than 'ke'

Computational steps:

- AUC is calculated using trapezoidal integration.

- The fraction absorbed is calculated from AUC and the terminal
  elimination rate constant.

- The remaining fraction is transformed using the natural logarithm.

- Linear regression of log(remaining fraction) against time yields 'ka'.

## References

Wagner JG and Nelson E (1963). Percent absorbed time plots derived from
blood level and/or urinary excretion data. Journal of Pharmaceutical
Sciences, 52(6), 610-611.

## Author

Zhonghui Huang

## Examples

``` r
# Simulated one-compartment oral absorption data
Dose <- 100
Fbio <- 1
Vd   <- 70
CL   <- 4
ka   <- 1.2
ke   <- CL / Vd
t  <- seq(0.5, 8, by = 0.5)
Ct <- (Fbio * Dose * ka) / (Vd * (ka - ke)) * (exp(-ke * t) - exp(-ka * t))

dat <- data.frame(TIME = t, DV = Ct)

ka_wanger_nelson(dat)
```
