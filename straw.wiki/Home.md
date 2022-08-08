<p align=center>
<img src="https://github.com/theaidenlab/straw/wiki/images/graphic_straw.png" alt="StrawLogo" align=center /> 
</p>

---
Straw is our API for **fast** data extraction for .hic files that provides **programmatic access** to the matrices. It is currently written in [C++](CPP) and [Python](Python), with support for [R](R). 

You can [download binaries](Download) compiled for different systems.

Straw works by reading the .hic file, finding the appropriate matrix and slice
of data, and printing the text in sparse upper triangular format.  It is not as fully featured as the Java [Juicebox command line tools](https://github.com/theaidenlab/juicebox/wiki/Data-Extraction);
in particular, it doesn't store the pointer data for all the matrices, only
the one queried, and currently we are only supporting matrices (not vectors).

Future versions may look more like the Java implementation. 

Special thanks to [Yue Wu](https://github.com/mikeaalv) for the initial Python port.

For questions, please use
[the Google Group](https://groups.google.com/forum/#!forum/3d-genomics).

If you use this tool in your work, please cite 

**Neva C. Durand, James T. Robinson, Muhammad S. Shamim, Ido Machol, Jill P. Mesirov, Eric S. Lander, and Erez Lieberman Aiden. "Juicebox provides a visualization system for Hi-C contact maps with unlimited zoom." Cell Systems 3(1), 2016.**
