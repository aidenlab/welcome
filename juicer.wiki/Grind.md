# Quick Description #
GRIND is a multi-threaded tool for traversing the Hi-C map and creating output files. These can then be used to train a neural network or feed into other tools.

See the more detailed usage [below](#detailed-usage)).

Upon a successful run of Grind (depending on parameters used), the output directory will contain a list of folders with many matrix files (npy or txt format) and summary files that have the filenames of these matrix files. Example:
```
.../outputDir/m250_v0/neural_net_summary.txt
.../outputDir/m250_v0/neural_net_run_2500/orig_462320_462445_matrix.npy  
.../outputDir/m250_v0/run_2500/orig_450960_451085_matrix.npy  
.../outputDir/m250_v0/run_2500/orig_353640_353765_matrix.npy
.../outputDir/m250_v0/run_2500/...[additional matrix files]...  
.../outputDir/m250_v0/run_2500/orig_453820_453945_matrix.npy  
.../outputDir/m250_v0/run_2500/orig_452160_452285_matrix.npy  
.../outputDir/m250_v0/run_2500/orig_21690_21830_matrix.npy  
```


## Examples ##
Note: In general, it's best to run several simultaneous jobs on a cluster (each handling a different chromosome/resolution) if massive datasets are being generated.

Here's an example of generating a training set from grind on a provided loop list with KR normalization at 5kb for chromosomes 1 and 2 with a stride of 3 with a dense (not just binary) label including amorphic labeling with 15x30 pixel regions (for the output matrices) :
```
grind -k KR -r 5000 -c 1,2 --stride 3 --dense-labels 
		--only-make-positives --amorphic-labeling --iterate-on-list 
                input.hic input.bedpe positions> 15,30,1000 output_directory
```

Here's an example of generating a training set from grind by traversing down the diagonal with horizontal wiggle of 10 pixels (+/- diagonal, so Hi-C diagonal not always exact diagonal of matrix) with KR normalization at 10kb for chromosomes 1 and 2 with a stride of 3 with a dense (not just binary) label with 150x300 pixel observed over expected regions (for the output matrices):
```
grind -k KR -r 5000 -c 1,2 --stride 3 --dense-labels --off-from-diagonal 10
		--observed-over-expected --amorphic-labeling --iterate-on-list 
                input.hic input.bedpe positions> 150,300,1000 output_directory
```


# Detailed Usage #
```
grind [-k NONE/KR/VC/VC_SQRT] [-r resolutions] [-c chromsomes] 
		[--stride increment] [--off-from-diagonal max-dist-from-diag] 
		[--img jpg] --observed-over-expected --dense-labels 
		--use-feature-orientation --only-make-positives 
		--amorphic-labeling --text-output 
		<mode> <hic file> <bedpe positions> <x,y,z> <directory>

		mode: 
		--iterate-down-diagonal 
		--iterate-on-list 
		--iterate-distortions
```
The required arguments are: 

* &lt;mode>: method used for generating examples; parameter behavior can vary based on the mode
** `iterate-down-diagonal`: traverse down the diagonal of a Hi-C map (+/- wiggle)
** `iterate-on-list`: traverse in and around a given set of regions (usually based on a feature annotation not near the diagonal)
** `iterate-distortions`:
* &lt;hic file>: the .hic file
* &lt;bedpe positions>: list of annotations in [bedpe format](https://github.com/theaidenlab/juicebox/wiki/Loading-Annotations-(Annotations-menu)#adding-2d-annotations).
* &lt;x,y,z>: generally, `x` and `y` define the number of row and columns respectively for the ouput matrix regions. `z` is not always used, but sometimes refers to the batch size for output directories, to determine when new directories should be created. 
* &lt;outputDirectory>: directory containing final outputs and all generated datasets.

The optional arguments are: 

* `-c <String(s)>` Chromosome(s) on which grind will be run. The number/letter for the chromosome can be used with or without appending the "chr" string. Multiple chromosomes can be specified using commas (e.g. 1,chr2,X,chrY). In general, it's best to provide a small number of chromosomes and instead run several simultaneous jobs on a cluster (each handling a different chromosome) if massive datasets are being generated. 
* `-r <int(s)>` Resolution(s) for which Grind will be run. Multiple resolutions can be specified using commas (e.g. 25000,10000,5000).
* `-k <NONE/VC/VC_SQRT/KR>` Normalizations (case sensitive) that can be selected. Generally, KR (Knight-Ruiz; default) balancing should be used when available. 
* `--stride <int>` Increment by which consecutive matrix regions will be traversed horizontally, vertically, and when applicable, diagonally.
* `--off-from-diagonal <int>` wiggle amount permitted around the diagonal specifically for `iterate-down-diagonal` mode; i.e. the diagonal does not need to be in the center of the output and can be offset by some amount. Large values should not be used and will slow down run time (are not a very efficient way to traverse the Hi-C map). 
* `--img <String>` can provide an image file type (e.g. jpg) to include outputs in such a format. However, certain assumptions are made for color scale, so this is not usually preferred. 
* `--observed-over-expected` Output an O/E map with log thresholding, rather than the normal observed map.
* `--dense-labels ` Use when detailed labeling is desired; i.e. not just that a feature is present, but the location of the feature within the matrix
* `--amorphic-labeling` Use to label the location of the feature within the matrix as a non-rectangle or non-square feature, but rather all enriched pixels greater than the mean of labeled pixels in the original feature definition.
* `--use-feature-orientation` should be used if features are sufficiently asymmetric and horizontal/vertical features need to be handled separately. 
* `--only-make-positives >` Generate only positive examples; no negative examples folder will be created.
* `--text-output>` The default output is for Grind to make .npy files for each matrix region; if a .txt file output is desired, use this flag.
