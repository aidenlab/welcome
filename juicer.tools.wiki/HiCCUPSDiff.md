## `Finding Differential Loops`

HiCCUPS Diff allows you to find differential loops between loop lists.

----
## `Usage`
```
hiccupsdiff [-m matrixSize] [-k normalization (NONE/VC/VC_SQRT/KR)] [-c chromosome(s)] [-f fdr] [-p peak width] [-i window] [-t thresholds] [-d centroid distances] <firstHicFile> <secondHicFile> <firstLoopList> <secondLoopList> <outputDirectory>
```

HiCCUPSDiff works by checking the loops called in each hic file on the other; it checks them by again calling HiCCUPS.  

----	

## `Required options`
`firstHicFile` - first [.hic file](Data) to compare
`secondHicFile` - second [.hic file](Data) to compare
`firstLoopList` - first loop list, that is, the result (`merged_loops`) of running [HiCCUPS](HiCCUPS) on the first .hic file
`secondLoopList` - second loop list, that is, the result (`merged_loops`) of running [HiCCUPS](HiCCUPS) on the second .hic file
`outputDirectory` - output directory. Will contain differentialLoopList1, containing loops that appear in the first loop list and are not present in the second hic file, and differentialLoopList2, containing loops that appear in the second loop list and are not present in the first hic file

----

## `Optional options`
This function takes optional HiCCUPS arguments; these are explained in the [HiCCUPS](HiCCUPS) section.