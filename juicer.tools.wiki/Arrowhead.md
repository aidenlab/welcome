# Quick Description #
Arrowhead is an algorithm for finding contact domains.

This is the usage that most users will likely use (more detailed usage [below](#detailed-usage)):
```
arrowhead <HiC file> <output_file>
```
Upon a successful run of Arrowhead, output_file will contain all the contact domains found along the diagonal in [this format](#domain-list-content).

## Examples ##

See this Colab notebook with an example run: [notebook](https://colab.research.google.com/drive/1XelZowBWxBghSyS11rvs90Zmazsj_HPh?usp=sharing)

```
arrowhead local/folder/HIC006.hic local/folder/contact_domains_list
```
This command will run Arrowhead on HIC006 at resolution 5 kB or 10 kB (depending on the map's resolution) and save all contact domains to the contact_domains_list file.

```
arrowhead https://hicfiles.s3.amazonaws.com/hiseq/gm12878/in-situ/combined_30.hic contact_domains_list
```
This command will run Arrowhead at resolution 5kB on the GM12878 HiC map (high resolution) and save all contact domains to the contact_domains_list file. Note: these are the settings used to generate the official GM12878 contact domain list. 

Default parameters for arrowhead described [below](#defaults).

# Detailed Usage #
```
arrowhead [-c chromosome(s)] [-m matrix size] [-r resolution] [--threads num_threads]
		[-k normalization (NONE/VC/VC_SQRT/KR)] <HiC file> 
		<output_file> [feature_list] [control_list]
```

The required arguments are:
 
* &lt;HiC file>: Address of HiC file which should end with ".hic". This is the file you would load into Juicebox. URLs or local addresses may be used. Running Arrowhead on MAPQ>30 and MAPQ>0 files generally gives comprable results.
* &lt;output_file>: Final list of all contact domains found by Arrowhead. Can be visualized directly in Juicebox as a [2D annotation](https://github.com/theaidenlab/juicebox/wiki/Loading-Annotations-(Annotations-menu)#adding-2d-annotations).

-- NOTE -- If you want to find scores for a feature and control list, both must be provided: 
* [feature_list]: Feature list of loops/domains for which block scores are to be calculated
* [control_list]: Control list of loops/domains for which block scores are to be calculated

The optional arguments are:

* `-c <String(s)>` Chromosome(s) on which Arrowhead will be run. The number/letter for the chromosome can be used with or without appending the "chr" string. Multiple chromosomes can be specified using commas (e.g. 1,chr2,X,chrY) 
* `-m <int>` Size of the sliding window along the diagonal in which contact domains will be found. Must be an even number as (m/2) is used as the increment for the sliding window. (Default 2000) 
* `-r <int>` resolution for which Arrowhead will be run. Generally, 5kB (5000) or 10kB (10000) resolution is used depending on the depth of sequencing in the HiC file(s). 
* `-k <NONE/VC/VC_SQRT/KR>` Normalizations (case sensitive) that can be selected. Generally, KR (Knight-Ruiz) balancing should be used when available. 
* `--threads <int>` Number of threads to use (Arrowhead is multi-threaded). As of Juicer Tools Version 1.13.02, the default number of threads used is 1. Passing in a value of 0 will result in the jar calculating the number of available threads. Passing in a value >0 will result in that value being used directly. 

## Defaults ##
Arrowhead uses the following parameters if optional flags are not provided.

Medium resolution maps: 
```
-c (all chromosomes) 
-m 2000 
-r 10000 
-k KR
```

High resolution maps: 
```
-c (all chromosomes) 
-m 2000 
-r 5000 
-k KR
```

### Domain List Content ###
The contact domain list created by Arrowhead will start with a header line, followed by a line for every contact domain. By default, the file should contain 12 fields per line in the following format:
```
chromosome1    x1    x2    chromosome2    y1    y2    color    
		corner_score    Uvar    Lvar    Usign    Lsign
```

Explanations of each field are as follows:
* chromosome = the chromosome that the domain is located on
* x1,x2/y1,y2 = the interval spanned by the domain (contact domains manifest as squares on the diagonal of a Hi-C matrix and as such: x1=y1, x2=y2)
* color = the color that the feature will be rendered as if loaded in Juicebox
* corner_score = the corner score, a score indicating the likelihood that a pixel is at the corner of a contact domain. Higher values indicate a greater likelihood of being at the corner of a domain (labeled `f1` in old format)
* Uvar  = the variance of the upper triangle (labeled `f2` in old format)
* Lvar = the variance of the lower triangle (labeled `f3` in old format)
* Usign = -1*(sum of the sign of the entries in the upper triangle) (labeled `f4` in old format)
* Lsign = sum of the sign of the entries in the lower triangle (labeled `f5` in old format)

See Section IV.a.3 of the Extended Experimental Procedures of <a href="http://www.cell.com/cell/abstract/S0092-8674(14)01497-4">Rao, Huntley et al. Cell 2014</a> for more details.
