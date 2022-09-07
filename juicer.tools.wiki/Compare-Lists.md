## Compare loop list Intro

The comparing lists option includes a few helper functions for analyses common with loop lists. In particular, it can check for exact differences (useful for debugging, not differential loops - for differential loops, use [HiCCUPS Diff](HiCCUPSDiff)) as well as convergent CTCF statistics for a loop list with motifs.

----

## Usage
```
compare [-m threshold] [-c chromosome(s)] <compareType> <genomeID> <list1> <list2> [output_path]
                 compareType:   0 - overlap/intersect within distance threshold
                                1 - comparison with ctcf motifs
                                2 - convergence calculation for list1 with ctcf motifs
```

----

## Examples
```
java -jar juicer_tools.jar compare -m 25000 -c 1,2,3 0 hg19 looplist1.bedpe looplist2.bedpe results_folder
```

This will find the exact difference between the looplists (allowing for a 25kb radius) and create file showing the loops that are in common, as well as different, between the two loop lists.

```
java -jar juicer_tools.jar compare 2 hg19 looplist1.bedpe looplist1.bedpe results_folder
```

This will calculate the number of convergent, divergent, and tandem oriented CTCF loops given a loop list containing motifs (i.e. after running [Motif Finder](MotifFinder)) and print out the statistics to the console.