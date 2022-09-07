## Aggregate Peak Analysis (APA) Overview 

From [Rao&Huntley et al., 2014](http://www.cell.com/cell/abstract/S0092-8674(14)01497-4): To measure the aggregate enrichment of a set of putative peaks in a contact matrix, we plot the sum of a series of submatrices derived from that contact matrix. Each of these submatrices is a 210 kb x 210 kb square centered at a single putative peak in the upper triangle of the contact matrix. The resulting APA plot displays the total number of contacts that lie within the entire putative peak set at the center of the matrix; the entry immediately to the right of center corresponds to the total number of contacts in the pixel set obtained by shifting the peak set 10 kb to the right; the entry two positions above center corresponds to an upward shift of 20 kb and so on. Focal enrichment across the peak set in aggregate manifests as larger values at the center of the APA plot.

----

## Quick Description

This is the usage that most users will likely use (more detailed usage [below](#detailed-usage)):
```
apa [-r resolution(s)] [-c chromosomes] [-u save_all_data] <HiC file(s)> <PeaksFile> <SaveFolder> 
```
By default, APA will save APA.png in the specified folder. This will contain just the genomewide aggregate plot with regional scores. For data from all potential models, use the `-u` flag. A description of all results after a successful run of APA are included [below](#description-of-results).

----
## Examples
```
apa HIC006.hic all_loops.txt results1
```

This command will run APA on HIC006 using loops from the all_loops files and save them under the results1 folder. 

```
apa https://hicfiles.s3.amazonaws.com/hiseq/gm12878/in-situ/combined.hic all_loops.txt results1 
```

This command will run APA on the GM12878 primary+replicate map using loops from the all_loops files and save them under the results1 folder. 

```
apa -r 10000,5000 -c 17,18 HIC006.hic+HIC007.hic all_loops.txt results 
```

This command will run APA at 50 kB resolution on chromosomes 17 and 18 for the summed HiC maps (HIC006 and HIC007) using loops from the all_loops files and save them under the results folder

----

## Detailed Usage
```
apa [-n minval] [-x maxval] [-w window] [-r resolution(s)] [-c chromosomes]
		[-k NONE/VC/VC_SQRT/KR] [-q corner_width] [-e include_inter_chr] [-u save_all_data]
        <hicFile(s)> <PeaksFile> <SaveFolder>
```
The required arguments are: 

* `<HiC file>`: Address of HiC file which should end with ".hic". This is the file you will load into Juicebox. URLs or local addresses may be used.
* `<PeaksFile>`: List of peaks in [standard 2D feature format](https://github.com/theaidenlab/juicebox/wiki/Loading-Annotations-(Annotations-menu)#adding-2d-annotations) 
* `<SaveFolder>`: Working directory where outputs will be saved 

The optional arguments are: 
* `-n <int>` minimum distance away from the diagonal. Used to filter peaks too close to the diagonal. Units are in terms of the provided resolution. (e.g. -n 30 @ resolution 5kB will filter loops within 30*(5000/sqrt(2)) units of the diagonal) 
* `-x <int>` maximum distance away from the diagonal. Used to filter peaks too far from the diagonal. Units are in terms of the provided resolution. (e.g. -n 30 @ resolution 5kB will filter loops further than 30*(5000/sqrt(2)) units of the diagonal) 
* `-w <int>` width of region to be aggregated around the specified loops (units of resolution) 
* `-r <int(s)>` resolution for APA; multiple resolutions can be specified using commas (e.g. 5000,10000) 
* `-c <String(s)>` Chromosome(s) on which APA will be run. The number/letter for the chromosome can be used with or without appending the "chr" string. Multiple chromosomes can be specified using commas (e.g. 1,chr2,X,chrY) 
* `-k <NONE/VC/VC_SQRT/KR>` Normalizations (case sensitive) that can be selected. Generally, KR (Knight-Ruiz) balancing should be used when available. 
* `-q <int(s)>` width of the corner regions corresponding to the respective resolution (position wise - i.e. should not be used without `-r` flag).
* `-e` will also run APA on any interchromosomal features annotated in the provided list. This is not used in the Cell 2014 and is an experimental feature at the request of users. APA statistics are not designed for interchromosomal regions, so use caution with this flag. Contact us with any questions.
* `-u` will save all data including plots for each chromosome and multiple hypothesis models.

Default settings of optional arguments: 
```
-n 30 
-x (infinity) 
-w 10 
-r 25000,10000,5000
-q 6,6,3
-c (all chromosomes) 
-k KR
```

----
## Description of Results

If run with the `-u` flag, results for APA will be split up into different folders for each of the different chromosomes (for example, the `X` folder has results for the X chromosome), and then aggregated over all chromosomes in the `gw` (genomewide) folder. Each folder has a summary text file called `measures.txt`.

The `measures.txt` file summarizes the APA scores for the "standard APA" tests. This text file has a set of measurements, detailed below:
* P2M 	: (Peak to Mean) the ratio of the central pixel to the mean of the remaining pixels.
* P2UL	: (Peak to Upper Left) the ratio of the central pixel to the mean of the mean of the pixels in the upper left corner
* P2UR      :(Peak to Upper Right) the ratio of the central pixel to the mean of the mean of the pixels in the upper right corner
* P2LL	(Peak to Lower Left) the ratio of the central pixel to the mean of the mean of the pixels in the lower left corner
* P2LR	:(Peak to Lower Right) the ratio of the central pixel to the mean of the mean of the pixels in the lower right corner
* ZscoreLL :(Zscore Lower Left) The Z-score of the of the central pixel relative to the all of the pixels in the lower left corner

To summarize APA, we recommend the user either use the P2LL or the ZscoreLL values from the genomewide APA results (in the `measures.txt` file in the `gw` folder) - this was what was done in <a href="http://www.cell.com/cell/abstract/S0092-8674(14)01497-4">Rao, Huntley et al. Cell 2014</a>. Values significantly above 1 for P2LL and significantly above 0 for ZscoreLL indicate enrichment.

More detail besides these summary measurements can be found in the remaining files. In each folder, there are a series of plots (.png); their associated data (the raw values of the plot) have the same filename but end in '.txt'. There are four different types of APA measurements that are run, and they are labeled in the files as "APA" (the standard measurement we recommend using), "normedAPA", "centerNormedAPA", and "rankAPA".

Each measurement shows a plot of a matrix, where the score of the putative loops is in the center of the matrix. A putative loop list which corresponds to true peaks in a Hi-C matrix should show marked visual enrichment at the center of these plots. Each plot shows four numbers in the corners of the plot. These numbers are the measured enrichment of the central pixel to all of the pixels inside the black square in the corner. The number that should be taken as the APA value is the number in the lower left corner, also denoted as P2LL (Peak to Lower Left) in the title. The title of the plot also gives "N", the number of putative loops that were used to create the plot. The "total" number is how many loops were given to the algorithm, and "filtered" and "unique" values give how many loops remain after filtering for distance threshold and filtering for uniqueness at a given resolution. 

The description of the four measurements are below:

* APA: This is the "standard APA" test, and is the recommended plot and measurement to use. It is also the measurement that was used in Rao & Huntley et al, Cell 2014. The matrix is created by summing together all submatrices around each individual putative peak, as described in VI.d.1 of the SI of Rao & Huntley et al, Cell 2014. 
* normedAPA: This is what is termed "normalized APA" in section VI.d.3 of the SI of Rao & Huntley et al, Cell 2014., where each submatrix is “normalized” by dividing all entries of the submatrix by the mean value of the submatrix, such that the mean value of the entries of the resulting submatrix is 1. 
* centerNormedAPA: An alternate version of APA where each submatrix is “normalized” by dividing all entries of the submatrix by the mean value of the central pixel. 
* rankAPA: An alternate version of APA where each submatrix is first converted to its percentile matrix - each value in the matrix is replaced with its percentile value within the matrix, such that a pixel with a value of for example 80.0 means that 80% of the other values in the matrix are lower in value than the value in the pixel. These percentile submatrices are then summed together.

The enhancement.txt contains a list of the P2M values for each of the standard APA submatrices (one value per putative loop).

See Section VI.d of the Extended Experimental Procedures of <a href="http://www.cell.com/cell/abstract/S0092-8674(14)01497-4">Rao, Huntley et al. Cell 2014</a> for more details.