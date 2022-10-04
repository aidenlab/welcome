## Installing Straw in R

Straw can be used in R through the `strawr` package. It has been tested with Windows, Mac, and Linux. It uses the [Rcpp](https://www.rcpp.org/) package for performance and reuse of C++ code. The latest official release can be installed from [CRAN](https://cran.r-project.org/):

    install.packages("strawr")

Alternatively, the latest version can be installed directly from GitHub:

    devtools::install_github("AidenLab/straw/R")

## Using Straw in R

The main function is simply named `straw`.

### Usage

    straw(norm, fname, chr1loc, chr2loc, unit, binsize, matrix = "observed")

### Arguments

`norm`

Normalization to apply. Must be one of NONE/VC/VC_SQRT/KR. VC is vanilla coverage, VC_SQRT is square root of vanilla coverage, and KR is Knight-Ruiz or Balanced normalization.

`fname`

path to .hic file

`chr1loc`

first chromosome location

`chr2loc`

second chromosome location

`unit`

BP (BasePair) or FRAG (FRAGment)

`binsize`

The bin size. By default, for BP, this is one of <2500000, 1000000, 500000, 250000, 100000, 50000, 25000, 10000, 5000> and for FRAG this is one of <500, 200, 100, 50, 20, 5, 2, 1>.

`matrix`

Type of matrix to output. Must be one of observed/oe/expected. observed is observed counts, oe is observed/expected counts, expected is expected counts.

### Example Usage

Here is an example usage with results:

    > head(strawr::straw("NONE", "/path/to/inter.hic", "1", "1", "BP", 2500000))
            x       y counts
    1       0       0    785
    2       0 2500000    122
    3 2500000 2500000    942
    4       0 5000000     43
    5 2500000 5000000    256
    6 5000000 5000000   1262

You can also use a URL for the input file:

    strawr::straw("NONE", "https://github.com/aidenlab/Juicebox/blob/master/data/inter.hic?raw=true", "1", "1", "BP", 2500000)

There are also auxiliary functions for reading various useful information from HIC files:

    >head(strawr::readHicChroms("https://github.com/aidenlab/Juicebox/blob/master/data/inter.hic?raw=true"))
      index name    length
    1     1    1 249250621
    2    10   10 135534747
    3    11   11 135006516
    4    12   12 133851895
    5    13   13 115169878
    6    14   14 107349540
    
    >strawr::readHicBpResolutions("https://github.com/aidenlab/Juicebox/blob/master/data/inter.hic?raw=true")
    [1] 2500000 1000000  500000  250000  100000   50000   25000   10000    5000
