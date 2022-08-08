<img src="https://github.com/theaidenlab/juicer/wiki/images/graphic_data.png" width="100%" alt="Data">
The data file formats used in the Juicer / Juicebox / Straw ecosystem are described below.

The Juicer data archive is available at [aidenlab.org/data.html](http://www.aidenlab.org/data.html) and consists of `.hic` files, described below.

# `.hic` files #
The `.hic` file is a highly compressed binary file that stores contact matrices from multiple resolutions in a clever way, allowing random access. 

To create a `.hic` file, use [Pre](Pre). To extract data from a .hic file, use [dump](Data-Extraction); or access the data directly with the [Straw API](http://github.com/theaidenlab/straw/wiki). All of the [feature annotation](Feature-Annotation) algorithms operate directly on `.hic` files. [Juicebox](https://github.com/theaidenlab/juicebox/wiki/Visualization) uses the fast querying capabilities of `.hic` files to make it possible to zoom in and out of many different resolutions quickly. 

The `.hic` file format is described in detail at: [https://github.com/aidenlab/hic-format](https://github.com/aidenlab/hic-format). The [Straw](https://github.com/aidenlab/straw) API can be used to read data from the .hic file into Java, Python, C++, R, and MATLAB.

# Hi-C contacts #
Hi-C contacts are represented as one line per read; the minimal necessary information is the chromosome and position of each read. [Pre](Pre) takes a number of [different possible formats](Pre#file-format) to represent Hi-C contacts.

# Fastq files #
These are the raw data files that come off the sequencer. They include the read name, the read (a string of A,C,T,G, or N) and base quality information. See [this article](https://en.wikipedia.org/wiki/FASTQ_format) for more information. Juicer takes `.fastq` files and transforms them into contact matrices stored in a `.hic` file. 



