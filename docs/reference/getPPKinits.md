# Automated pipeline for generating initial estimates in population PK models

Provides a unified and fully automated workflow to generate initial
pharmacokinetic and residual variability parameters for population PK
models using concentration–time data from bolus, infusion, or oral
administration.

## Usage

``` r
getPPKinits(dat, control = initsControl(), ncores = 2, verbose = TRUE)
```

## Arguments

- dat:

  A data frame containing pharmacokinetic records in standard nlmixr2
  format, including ID, TIME, EVID, and DV.

- control:

  A list created by
  [`initsControl()`](https://init.nlmixr2auto.org/reference/initsControl.md)
  specifying configuration for pooling, non-compartmental analysis,
  steady-state detection, fallback rules, statistical model components,
  and parameter selection metrics.

- ncores:

  Number of cores to use for parallelization, passed to `rxControl()`.
  Default is 2.

- verbose:

  Logical (default = TRUE); when TRUE, displays key progress messages
  and stepwise updates during the initialization process. When FALSE,
  the function runs quietly without printing intermediate information.

## Value

An object of class `getPPKinits` containing recommended initial
parameter estimates, intermediate results, and computation diagnostics.

## Details

The pipeline integrates four model-informed analytical components
applied to raw or pooled concentration–time profiles:

1.  Adaptive single-point methods

2.  Naive pooled graphic methods

3.  Naive pooled non-compartmental analysis (NCA) with optional
    Wagner–Nelson Ka calculation for oral dosing

4.  Parameter sweeping across one-, two-, three-compartment and
    Michaelis–Menten models

In addition to structural PK parameters, the framework also initializes
statistical model components:

- Inter-individual variability (IIV): pragmatic fixed \\\omega^2\\
  values are assigned to random effects.

- Residual unexplained variability (RUV): estimated either using a
  data-driven method based on trimmed residual summaries or a
  fixed-fraction approach consistent with NONMEM User Guide
  recommendations.

- Model applicability: the automated and model-informed strategy
  generates robust initial values suitable for both linear and nonlinear
  mixed-effects pharmacokinetic models.

## See also

[`initsControl`](https://init.nlmixr2auto.org/reference/initsControl.md),
[`run_single_point`](https://init.nlmixr2auto.org/reference/run_single_point.md),
[`run_graphcal`](https://init.nlmixr2auto.org/reference/run_graphcal.md),
[`run_pooled_nca`](https://init.nlmixr2auto.org/reference/run_pooled_nca.md),
[`sim_sens_1cmpt_mm`](https://init.nlmixr2auto.org/reference/sim_sens_1cmpt_mm.md),
[`sim_sens_2cmpt`](https://init.nlmixr2auto.org/reference/sim_sens_2cmpt.md),
[`sim_sens_3cmpt`](https://init.nlmixr2auto.org/reference/sim_sens_3cmpt.md),
[`metrics.`](https://init.nlmixr2auto.org/reference/metrics..md)

## Author

Zhonghui Huang

## Examples

``` r
# \donttest{
getPPKinits(pheno_sd[pheno_sd$ID<11,])
# }
```
