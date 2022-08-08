The eigenvector can be used to delineate compartments in Hi-C data at coarse resolution; the sign of the eigenvector typically indicates the compartment. The eigenvector is the first principal component of the [Pearson's](Pearsons) matrix.

# Usage #
```
eigenvector <NONE/VC/VC_SQRT/KR> <hicFile(s)> <chr> <BP/FRAG> <binsize> [outfile]
```

# Examples #
```
java -jar juicer_tools.jar eigenvector KR HIC001.hic 1 BP 1000000
```

This will calculate the eigenvector of chromosome 1 with KR normalization at 1Mb resolution and print to standard out

```
java -jar juicer_tools.jar eigenvector VC HIC001.hic X BP 5000 eigen.txt
```

This will calculate the eigenvector of chromosome X with VC normalization at 5Kb resolution and print to eigen.txt.