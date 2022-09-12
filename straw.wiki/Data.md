## `hic` format
The `hic` file is a highly compressed binary file that stores contact matrices from multiple resolutions in a clever way, allowing random access. The file format is described in detail on [GitHub](https://github.com/aidenlab/hic-format).

The primary way to create a `hic` file is using the [Pre](Pre) command. [Pre](Pre) takes a number of [different possible formats](Pre#file-format) to represent Hi-C data. Hi-C contacts are represented as one line per read pair; the minimal necessary information is the chromosome and position of each read.

Various tools, including [Juicebox Web and Juicebox Desktop](juicebox.wiki/Juicebox_intro.md) can visualize Hi-C data directly, and allow users to explore the contact maps, zooming in and out across many resolutions quickly. Most [feature annotation](Feature-Annotation) algorithms operate directly on `hic` files, including HiCCUPS, Arrowhead, POSSUMM, SLICE, and more. For advanced programmatic access and extracting data from a .hic file, use [Straw](straw.wiki/Home.md). 



