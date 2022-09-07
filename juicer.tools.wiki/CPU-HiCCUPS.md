## Important
HiCCUPS CPU versions prior to 1.19.01 had a bug where not all potential regions were queried, so only the latest version should be used. Also, note that the CPU version remains experimental and that GPU HiCCUPS is the standard. Consider using the free GPUs on Google Colab. Here's an example run of HiCCUPS and Arrowhead: [notebook](https://colab.research.google.com/drive/1XelZowBWxBghSyS11rvs90Zmazsj_HPh?usp=sharing)

----
## General
HiCCUPS was developed to run on GPUs, as it is a computationally intensive algorithm which analyzes all intrachromosomal spaces to identify areas of local enrichment for peak identification. However, many groups may not have access to a GPU, and as such, we have introduced a modified version of HiCCUPS which will run on CPUs.

The primary difference involves restricting the search space of the HiCCUPS algorithm to only search for peaks within 8MB of the diagonal. In practice, we do see that the vast majority of loops (especially CTCF mediated chromatin loops) are within a few megabases of the diagonal. 

"The vast majority of peaks (98%) reflected loops between loci that are <2 Mb apart" [Rao and Huntley et al. 2014](https://www.cell.com/abstract/S0092-8674%2814%2901497-4)

However, due to this restriction of the intrachromosomal search space, the FDR thresholds calculated are slightly different from running the full GPU-based HiCCUPS. In addition, since the area of the region analyzed varies with the `-m` flag, slight differences in loops may result when using different sub-matrix sizes (area of window/region examined at a given time). 

----
## Usage
The CPU version of HiCCUPS uses exactly the same inputs (including all the optional parameters) as regular [HiCCUPS](HiCCUPS), with the addition of the `--cpu` flag
```
hiccups --cpu [--threads num_threads] [-m matrixSize] [-c chromosome(s)] [-r resolution(s)] 
		<HiC file> <outputDirectory> 
```

You can also specify the number of threads to use with the `--threads` flag (CPU HiCCUPS is multi-threaded). As of Juicer Tools Version 1.13.02, the default number of threads used is 1. Passing in a value of 0 will result in the jar calculating the number of available threads. Passing in a value >0 will result in that value being used directly. 

You may also choose to run GPU-based HiCCUPS using the same restriction of searching within 8MB of the diagonal. This results in identical results with CPU HiCCUPS, and can be run using the `--restrict` flag.

```
hiccups --restrict [-m matrixSize] [-c chromosome(s)] [-r resolution(s)]
                <HiC file> <outputDirectory>
```

----
## Example of Differences

Using the cohesin-degron maps from [Rao et al. 2017](https://www.cell.com/cell/pdf/S0092-8674(17)31120-0.pdf), regular GPU-based HiCCUPS finds 3444 loops in the untreated megamap and 350 loops in the treated megamap. CPU-based HiCCUPS (and restricted GPU-based HiCCUPS) finds 3300 loops in the untreated megamap and 239 loops in the treated megamap.

Of the loops identified in the untreated megamap, 3167 match exactly and are identical; 77 are within a 10kB tolerance region; 200 are unique to the GPU version and 56 are unique to the CPU version. 

Of the loops identified in the treated megamap, 186 match exactly and are identical; 38 are within a 10kB tolerance region; 126 are unique to the GPU version and 15 are unique to the CPU version.