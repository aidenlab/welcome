Juicer is designed to be a simple one-click end-to-end pipeline that will complete all of your analysis (given a successful installation). This includes building the `hic` file and running downstream analysis (e.g. HiCCUPS, Arrowhead, etc.). 

However, you may want to build custom `hic` files or run downstream analysis tools with different parameters - that is what this section is designed for. 

The [Pre](Pre) command will create `hic` files from a list of contacts. Downstream feature annotation algorithms (HiCCUPS, Arrowhead, APA, etc) operate on these `hic` files directly. Most of the algorithms can work with URLs as well, so you can use the links in the [Hi-C Archive](http://aidenlab.org/data.html) to operate directly on that data without downloading it.
