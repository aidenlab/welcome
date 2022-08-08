Straw is compatible with R via the Rcpp library.  Usage is very similar to the [examples on the C++ page](https://github.com/theaidenlab/straw/wiki/CPP#running).  Future versions might use a different signature to call the function.

```
library(Rcpp)
sourceCpp("straw-R.cpp")
A<-straw_R("NONE drosophila.hic arm_2L arm_2L BP 100000")
```
In the above example, A is a data frame containing the counts information:

```
> head(A)
        x        y counts
1  800000  4700000     77
2       0        0  41105
3 5500000  8100000     82
4 2700000  8300000     85
5 5700000 17700000     11
6 3000000 16500000     27
```

# Troubleshooting #
Please see this <a href="http://aidenlab.org/forum.html?place=msg%2F3d-genomics%2FsD2JOOoLBZw%2F3M1xgAlOBAAJ">forum post</a> for a solution to a compilation error that some users have experienced.