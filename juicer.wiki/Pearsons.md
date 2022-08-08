The Pearson's correlation matrix of the Observed/Expected can be calculated on any intra-chromosomal matrix. Please be warned that higher resolution data will take much longer to calculate.

# Usage #
```
pearsons <NONE/VC/VC_SQRT/KR> <hicFile(s)> <chr> <BP/FRAG> <binsize> [outfile]  
```

# Examples #
```
java -jar juicer_tools.jar pearsons KR HIC001.hic 1 BP 1000000
```
This will calculate the Pearson's correlation matrix of the Observed/Expected of chromosome 1, KR normalized, at 1MB resolution.  The resulting dense matrix will be printed to standard out.

```
java -jar juicer_tools.jar pearsons NONE HIC001.hic X BP 25000 pearsons_25Kb.txt
```
This will calculate the Pearson's correlation matrix of the Observed/Expected of chromosome X, with no normalization, at 25KB resolution.  The resulting dense matrix will be printed to the text file pearsons_25Kb.txt.

# Binary format #
Generally Juicebox will not display high resolution maps, because they take a long time to calculate. However, Juicebox does look for precalculated maps when it tries to display Pearsons at high resolution.

If your directory is "MyHiCMap" and contains your file "HIC001.hic", you should have a subdirectory for every chromosome needed:
```
MyHiCMap/
   HIC001.hic
   1/ 
   2/
   3/
   ...
   X/
```
Then your Pearsons maps should be named "pearsons_*resolution*_*norm*.bin"
For example:

```
java -jar juicer_tools.jar pearsons VC HIC001.hic 3 BP 100000 3/pearsons_100000_VC.bin
```
This will calculate the Pearson's correlation matrix of the Observed/Expected of chromosome 3, VC normalized, at 100KB resolution.  The resulting dense matrix will be stored in the binary file pearsons_100000_VC.bin in block format. This file should be saved in the folder "3", for chromosome 3.
