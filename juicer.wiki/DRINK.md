DRINK (Differentiating Ratios with INtrachromosomal Kmeans) is _**experimental**_ code that compares similar maps and uses multi-threaded K-means clustering to detect which regions are different between the provided maps. An arbitrary number of maps may hypothetically be provided. The first map provided is assumed to represent a relative control for the other datasets. DRINK-ing is most helpful in cases where the maps appear to be fairly similar overall and have relatively minor differences.

DRINK does not intrinsically identify subcompartments.

The code runs fairly quickly, completing in under two minutes at 50kB resolution with 2-3 maps. Using higher resolutions or providing several maps may require additional RAM requirements.

# Usage #

```
drink [-r resolution] [-k NONE/VC/VC_SQRT/KR] [-m num_clusters] 
		<input1.hic+input2.hic+input3.hic...> <output_directory>
```

The required arguments are: 

* &lt;input1.hic+input2.hic+input3.hic>: List of .hic files paths joined with '+'. The first .hic file is assumed to be a relative control. DRINK has so far only been tested with MAPQ>30 hic files.
* &lt;output_directory>: Directory containing final cluster assignments as colored .bed files, as well as diff vectors relative to the control .hic file, which can be visualized directly in Juicebox as [1D annotations](https://github.com/aidenlab/Juicebox/wiki/Loading-Annotations-(Annotations-menu)#loading-1d-tracks). 

The optional arguments are: 
* `-m <int>` Maximum number of clusters used by the Kmeans algorithm. Values above 20 may be used, but colors in the .bed file may get reused. 
* `-r <int>` a single resolution for which DICE will be run, generally 100000 (100kB) or 50000 (50kB). 
* `-k <NONE/VC/VC_SQRT/KR>` Normalizations (case sensitive) that can be selected. Generally, KR (Knight-Ruiz) balancing should be used when available.

## Examples ##

```
drink gm12878_mega.hic+gm12878_primary.hic+gm12878_replicate.hic cluster_results
```


```
drink -m 20 degron_untreated.hic+degron_6hr_treated.hic degron_cluster_results
```
