# Bin time-concentration data using quantile or algorithmic binning

Bins data by time using either equal-frequency (quantile) binning or
algorithmic binning methods.

## Usage

``` r
bin.time(
  dat,
  nbins = "auto",
  bin.method = c("quantile", "jenks", "kmeans", "pretty", "sd", "equal", "density")
)
```

## Arguments

- dat:

  A data frame containing PK data. Must include:

  - tad: time after dose

  - DVstd: standardized concentration (DV/dose)

  - EVID: optional event ID column used to filter observations (EVID ==
    0)

- nbins:

  Number of bins or "auto". If numeric with `bin.method = "quantile"`,
  specifies equal-frequency bins. If "auto", 10 bins are used for
  quantile; otherwise binning is determined by
  [`vpc::auto_bin`](https://rdrr.io/pkg/vpc/man/auto_bin.html). Numeric
  nbins for non-quantile methods is passed to
  [`vpc::auto_bin`](https://rdrr.io/pkg/vpc/man/auto_bin.html).

- bin.method:

  Binning strategy (default = "quantile"). Available options are:

  - quantile: equal-frequency binning by empirical quantiles

  - jenks: natural breaks minimizing within-bin variance

  - kmeans, pretty, sd, equal, density: alternative binning methods from
    vpc::auto_bin

## Value

A list containing summary results of the time-concentration binning
process.

## Details

Supports quantile-based binning and other data-driven methods (jenks,
kmeans, pretty, sd, equal, density), with optional automatic bin count
selection.

## See also

[`vpc::auto_bin`](https://rdrr.io/pkg/vpc/man/auto_bin.html)

## Author

Zhonghui Huang

## Examples

``` r
dat <- Bolus_1CPT
dat <- nmpkconvert(dat)
dat <- calculate_tad(dat)
dat$DVstd <- dat$DV / dat$dose
bin.time(dat)
```
