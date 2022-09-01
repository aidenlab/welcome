## `hic` file format
The `hic` file is a highly compressed binary file that stores contact matrices from multiple resolutions in a clever way, allowing random access. The file format is described in detail on [GitHub](https://github.com/aidenlab/hic-format).

The primary way to create a `hic` file is using the [Pre](Pre) command. [Pre](Pre) takes a number of [different possible formats](Pre#file-format) to represent Hi-C data. Hi-C contacts are represented as one line per read pair; the minimal necessary information is the chromosome and position of each read.

Various tools, including [Juicebox Web and Juicebox Desktop](juicebox.wiki/Juicebox_intro.md) can visualize Hi-C data directly, and allow users to explore the contact maps, zooming in and out across many resolutions quickly. Most [feature annotation](Feature-Annotation) algorithms operate directly on `hic` files, including HiCCUPS, Arrowhead, POSSUMM, SLICE, and more. For advanced programmatic access and extracting data from a .hic file, use [Straw](straw.wiki/Home.md). 

----

## `bedpe` file format 
The [`bedpe`](https://bedtools.readthedocs.io/en/latest/content/general-usage.html#bedpe-format) format is used for annotating 2D features, such as chromatin loop and contact domains. Bedpe files are tab-delimited. The header line looks like this:

```
#chr1  x1	 x2	    chr2   y1	      y2	  name	score  strand1  strand2	color [optional fields]
chr5   85000000  89000000   chr5   85000000   89000000    .     .      .        .       255,0,0
``` 

Many of our software tools use `bedpe` files as direct inputs or outputs.

----

## `Fastq` files
These are the raw data files that come off the sequencer. They include the read name, the read (a string of A,C,T,G, or N) and base quality information. See [this article](https://en.wikipedia.org/wiki/FASTQ_format) for more information. Juicer takes `.fastq` files and transforms them into contact matrices stored in a `.hic` file. 



