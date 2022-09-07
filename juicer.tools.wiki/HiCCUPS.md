## Finding Loops (GPU)
HiCCUPS is an algorithm for finding chromatin loops.

This is the usage that most users will likely use (more detailed usage [below](#detailed-usage)):
```
hiccups [-m matrixSize] [-c chromosome(s)] [-r resolution(s)] 
		<HiC file> <outputDirectory> 
```

Upon a successful run of HiCCUPS (depending on parameters used), the outputDirectory will contain something similar to:
```
.../outputDirectory/
.../outputDirectory/merged_loops (the final looplist - this is likely what you'll use)
.../outputDirectory/enriched_pixels_10000
.../outputDirectory/enriched_pixels_5000 (contains raw enriched pixels from GPU)
.../outputDirectory/fdr_thresholds_10000 
.../outputDirectory/fdr_thresholds_5000 (threshold values used to calculate enrichment)
.../outputDirectory/postprocessed_pixels_10000
.../outputDirectory/postprocessed_pixels_5000 (clustered pixels for each resolution)

```
The merged_loops file uses [this format](#loop-list-content).

----

## Examples
NOTE: HiCCUPS will choose appropriate defaults for HiC files if no specifications are given

```
hiccups local/folder/HIC006.hic local/folder/hiccups_results
```

This command will run HiCCUPS on HIC006 and save all found loops in the hiccups_results folder. It will check the density of the Hi-C map to determine appropriate parameters for running HiCCUPS on the provided .hic file.

```
hiccups -m 1024 -r 5000,10000 -c 22 https://hicfiles.s3.amazonaws.com/hiseq/gm12878/in-situ/combined_30.hic hiccups_results
```

This command will run HiCCUPS on chromosome 22 of GM12878 using [default parameters](#defaults) for 5kB and 10kB resolutions. The results will be merged and saved in the hiccups_results folder. The GPU will use matrix slices of size 1024x1024 (likely speeding up the computation on a dedicated GPU).

----
## Detailed Usage
```
hiccups [-m matrixSize] [-c chromosome(s)] [-r resolution(s)] [--threads num_threads]
		[-k normalization (NONE/VC/VC_SQRT/KR)] [-f fdr] 
		[-p peak width] [-i window] [-t thresholds] 
		[-d centroid distances] <HiC file> <outputDirectory> [specified_loop_list]
```
The required arguments are: 

* &lt;HiC file>: Address of HiC file which should end with ".hic". This is the file you will load into Juicebox. URLs or local addresses may be used. HiCCUPS should be run using MAPQ>30 hic files.
* &lt;outputDirectory>: Directory containing final merged list of all loops found by HiCCUPS. Can be visualized directly in Juicebox as a [2D annotation](https://github.com/theaidenlab/juicebox/wiki/Loading-Annotations-(Annotations-menu)#adding-2d-annotations). By default, various values critical to the HICCUPS algorithm are saved as attributes for each loop found. These can be disabled using the suppress flag below. Intermediate files created by HiCCUPS (raw pixels from GPU, clustered pixels for each resolution, and FDR thresholds) will also be saved in this directory.

The optional arguments are: 
* `specified_loop_list <Loop List>` is an optional positional argument which should point to a [Juicebox formatted loop list](https://github.com/theaidenlab/juicebox/wiki/Loading-Annotations-(Annotations-menu)#adding-2d-annotations). HiCCUPS will then return enrichments for these specified loops for each resolution. Starting with version 1.12.03, the given pixels are post-processed at each resolution and the results are merged across resolutions. This will create additional files in addition to the ones created in prior versions. CPU version only searches near the diagonal (in order to run in a reasonable amount of time), so it will not include regions far from the diagonal.

* `-m <int>` Maximum size of the submatrix within the chromosome passed on to GPU (Must be an even number greater than 40 to prevent issues from running the CUDA kernel). The upper limit will depend on your GPU. Dedicated GPUs should be able to use values such as 500, 1000, or 2048 without trouble. Integrated GPUs are unlikely to run sizes larger than 90 or 100. Matrix size will not effect the result, merely the time it takes for hiccups. Larger values (with a dedicated GPU) will run fastest. 
* `-c <String(s)>` Chromosome(s) on which HiCCUPS will be run. The number/letter for the chromosome can be used with or without appending the "chr" string. Multiple chromosomes can be specified using commas (e.g. 1,chr2,X,chrY) 
* `-r <int(s)>` Resolution(s) for which HiCCUPS will be run. Multiple resolutions can be specified using commas (e.g. 25000,10000,5000). Due to the nature of DNA looping, it is unlikely that loops will be found at lower resolutions (i.e. 50kB or 100kB) IMPORTANT: if multiple resolutions are used, the flags below can be configured so that different parameters are used for the different resolutions. 
* `-k <NONE/VC/VC_SQRT/KR>` Normalizations (case sensitive) that can be selected. Generally, KR (Knight-Ruiz) balancing should be used when available. 
* `-f <int(s)>` FDR values actually corresponding to max_q_val (i.e. for 1% FDR use 0.01, for 10%FDR use 0.1). Different FDR values can be used for each resolution using commas. (e.g "-r 5000,10000 -f 0.1,0.15" would run HiCCUPS at 10% FDR for resolution 5000 and 15% FDR for resolution 10000) 
* `-p <int(s)>` Peak width used for finding enriched pixels in HiCCUPS. Different peak widths can be used for each resolution using commas. (e.g "-r 5000,10000 -p 4,2" would run at peak width 4 for resolution 5000 and peak width 2 for resolution 10000) 
* `-i <int(s)>` Window width used for finding enriched pixels in HiCCUPS. Different window widths can be used for each resolution using commas. (e.g "-r 5000,10000 -p 10,6" would run at window width 10 for resolution 5000 and window width 6 for resolution 10000) 
* `-t <floats>` Thresholds for merging loop lists of different resolutions. Four values must be given, separated by commas (e.g. 0.02,1.5,1.75,2). These thresholds (in order) represent: > threshold allowed for sum of FDR values of the horizontal, vertical, donut, and bottom left filters (an accepted loop must stay below this threshold) > threshold ratio that both the horizontal and vertical filters must exceed > threshold ratio that both the donut and bottom left filters must exceed > threshold ratio that at least one of the donut and bottom left filters must exceed 
* `-d <ints>` Distances used for merging nearby pixels to a centroid. Different distances can be used for each resolution using commas. (e.g "-r 5000,10000 -d 20000,21000” would merge pixels within 20kB of each other at 5kB resolution and within 21kB at 10kB resolution.
* `--threads <int>` Number of threads to use (HiCCUPS is multi-threaded). As of Juicer Tools Version 1.13.02, the default number of threads used is 1. Passing in a value of 0 will result in the jar calculating the number of available threads. Passing in a value >0 will result in that value being used directly. 

----
## Detailed Example

See this Colab notebook with an example run: [notebook](https://colab.research.google.com/drive/1XelZowBWxBghSyS11rvs90Zmazsj_HPh?usp=sharing)

```
hiccups -m 500 -r 5000,10000 -f 0.1,0.1 -p 4,2 -i 7,5 -d 20000,20000,0 -c 22 HIC006.hic all_hiccups_loops
```

This command will run HiCCUPS on chromosome 22 of HIC006 at 5kB and 10kB resolution using the following values: 
* >5kB: fdr 10%, peak width 4, window width 7, and centroid distance 20kB 
* >10kB: fdr 10%, peak width 2, window width 5, and centroid distance 20kB 
The resulting merged loop list as well as intermediate results will be saved in the all_hiccups_loops folder. 

Note that these are values used for generating the GM12878 loop list, and that we could have also simply called
```
hiccups -m 500 -r 5000,10000 -c 22 HIC006.hic all_hiccups_loops
```
to achieve the same results.

----

## Defaults

These are the default parameters in for HiCCUPS described with all the available flags, as described in <a href="http://www.cell.com/cell/abstract/S0092-8674(14)01497-4">Rao, Huntley et al. Cell 2014</a>.

Medium resolution maps: 
```
-m 512 
-c (all chromosomes) 
-r 5000,10000,25000 
-k KR 
-f .1,.1,.1 
-p 4,2,1 
-i 7,5,3 
-t 0.02,1.5,1.75,2 
-d 20000,20000,50000 
```

High resolution maps: 
```
-m 512 
-c (all chromosomes) 
-r 5000,10000 
-k KR 
-f .1,.1 
-p 4,2 
-i 7,5 
-t 0.02,1.5,1.75,2 
-d 20000,20000,50000
```

----
## Loop List Content

The merged loop list created by HiCCUPS will start with a header line, followed by a line for every loop. By default, the file should contain 20 fields per line in the following format:

```
chromosome1    x1    x2    chromosome2    y1    y2    color    observed
		expected_bottom_left    expected_donut    expected_horizontal    expected_vertical    
		fdr_bottom_left    fdr_donut    fdr_horizontal    fdr_vertical    
		number_collapsed    centroid1    centroid2    radius
```

Note: If you also run Motif Finder, [additional fields](MotifFinder#result) will be created.

Explanations of the 20 fields are as follows:
* chromosome = the chromosome that the loop is located on
* x1,x2 = the coordinates of the upstream locus corresponding to the peak pixel
* y1,y2 = the coordinates of the downstream locus corresponding to the peak pixel
* color = the color that the feature will be rendered as if loaded in Juicebox
* observed = the raw observed counts at the peak pixel
* expected_[bottom_left, donut, horizontal, vertical] = the expected counts calculated using the [bottom_left, donut, horizontal, vertical] filter
* fdr_[bottom_left, donut, horizontal, vertical] = the q-value of the loop calculated using the [bottom_left, donut, horizontal, vertical] filter 
* number_collapsed = the number of pixels that were clustered together as part of the loop call 
* centroid1 = the upstream coordinate of the centroid of the cluster of pixels corresponding to the loop 
* centroid2 = the downstream coordinate of the centroid of the cluster of pixels corresponding to the loop 
* radius = the Euclidean distance from the centroid of the cluster of pixels to the farthest pixel in the cluster of pixels

See section VI.a.5.iv of the Extended Experimental Procedures of <a href="http://www.cell.com/cell/abstract/S0092-8674(14)01497-4">Rao, Huntley et al. Cell 2014</a> for more details.