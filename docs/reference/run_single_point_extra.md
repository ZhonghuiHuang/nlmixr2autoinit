# Perform extended single-point pharmacokinetic calculations

Extended single-point pharmacokinetic analysis for deriving CL, Vd, and
ka

## Usage

``` r
run_single_point_extra(
  dat = NULL,
  half_life = NULL,
  single_point_base.lst = NULL,
  route = c("bolus", "oral", "infusion"),
  dose_type = NULL,
  pooled_ctrl = pooled_control(),
  ssctrl = ss_control()
)
```

## Arguments

- dat:

  A data frame containing raw time–concentration data in the standard
  nlmixr2 format.

- half_life:

  Optional numeric value representing the elimination half-life of the
  drug. If not provided, half-life is estimated within
  [`run_single_point_base()`](https://init.nlmixr2auto.org/reference/run_single_point_base.md)
  using [`get_hf()`](https://init.nlmixr2auto.org/reference/get_hf.md)
  applied to the pharmacokinetic observations.

- single_point_base.lst:

  A list object returned from the base single-point calculation that
  includes input data, preprocessing information, and initial estimates
  of CL and Vd. If not supplied, the function will internally call the
  base routine using dat.

- route:

  Character string specifying the route of administration. Must be one
  of "bolus", "oral", or "infusion".

- dose_type:

  Classified as "first_dose", "repeated_doses", or "combined_doses"
  based on whether observed concentrations occur following the first
  administration, during repeated dosing, or across both contexts. This
  parameter is passed directly to
  [`run_single_point_base()`](https://init.nlmixr2auto.org/reference/run_single_point_base.md).

- pooled_ctrl:

  A list of pooled-analysis control options created using
  [`pooled_control()`](https://init.nlmixr2auto.org/reference/pooled_control.md).
  These control time binning and time-after-dose rounding when pooled
  summaries are required.

- ssctrl:

  A list of steady-state control options created using
  [`ss_control()`](https://init.nlmixr2auto.org/reference/ss_control.md).
  These govern assumptions and thresholds used when interpreting
  steady-state behavior in single-point logic.

## Value

A list containing:

- singlepoint.results: A data frame with estimated ka, CL, Vd,
  computation start time, processing time, and a descriptive message of
  the applied logic.

- dat: The dataset used for processing.

- single_point.ka.out: Output used for estimating the absorption rate
  constant (for oral administration), if applicable.

- single_point_cl_df: Data used for clearance estimation.

- single_point_vd_df: Data used for volume of distribution estimation.

- approx.vc.out: Data used for estimating the volume of distribution
  from maximum concentration (Cmax) and dose when needed.

## Details

The function derives pharmacokinetic parameters using the following
logic:

- When both clearance (CL) and volume of distribution (Vd) are available
  from the base calculation, these values are directly used without
  modification.

- If Vd is missing but CL and elimination half-life are provided, Vd is
  calculated using: \$\$V_d = \frac{CL \cdot t\_{1/2}}{\ln(2)}\$\$

- If CL is missing but Vd and half-life are available, CL is calculated
  using: \$\$CL = \frac{V_d \cdot \ln(2)}{t\_{1/2}}\$\$

- If both CL and Vd are unavailable but half-life is provided, Vd is
  estimated using dose and Cmax: \$\$V_d =
  \frac{\mathrm{Dose}}{C\_{\mathrm{max}}}\$\$ and CL is subsequently
  derived: \$\$CL = \frac{V_d \cdot \ln(2)}{t\_{1/2}}\$\$

- For oral administration, the absorption rate constant (ka) is
  estimated using a solution-based approach implemented in
  [`run_ka_solution()`](https://init.nlmixr2auto.org/reference/run_ka_solution.md).
  Only concentration–time data from the absorption phase are used,
  defined as time after dose (tad) less than 20% of the terminal
  half-life and occurring prior to Tmax, where absorption is the
  dominant process.

The function supports bolus, oral, and infusion administration routes.
For oral dosing, only data within the absorption phase are used to
estimate the absorption rate constant (ka), specifically using
concentration-time observations prior to the maximum concentration
(Tmax).

## See also

[`run_single_point_base`](https://init.nlmixr2auto.org/reference/run_single_point_base.md),
[`run_single_point`](https://init.nlmixr2auto.org/reference/run_single_point.md),
[`run_ka_solution`](https://init.nlmixr2auto.org/reference/run_ka_solution.md)

## Author

Zhonghui Huang

## Examples

``` r
dat <- Bolus_1CPT
out <- processData(dat)
fdat <- out$dat
froute <- out$Datainfo$Value[out$Datainfo$Infometrics == "Dose Route"]
half_life <- get_hf(dat = fdat)$half_life_median
run_single_point_extra(
  dat = fdat,
  half_life = half_life,
  single_point_base.lst = run_single_point_base(
    dat = fdat,
    half_life = half_life,
    route = froute
  ),
  route = froute
)
```
