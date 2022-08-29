# Juicer #
<img src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicer.images/graphic_juicer.png" width="100%" alt="Overview"/>

# What is Juicer? #
Juicer is a one-click pipeline for processing terabase scale Hi-C datasets. Using Juicer, you can

- Go from raw fastq files to Hi-C maps binned at many resolutions
- Automatically annotate loops and contact domains with the [Juicer tools](Juicer-Tools-Quick-Start)
- Run the pipeline [in the cloud](Running-Juicer-on-Amazon-Web-Services), on [LSF](https://github.com/theaidenlab/juicer/tree/master/LSF), [Univa](https://github.com/theaidenlab/juicer/tree/master/UGER), or [SLURM](https://github.com/theaidenlab/juicer/tree/master/SLURM), or on a single [CPU](https://github.com/theaidenlab/juicer/tree/master/CPU)

**Juicer** creates [hic files](Data) from raw (unaligned) reads derived from a Hi-C experiment. 

**[Juicer Tools](Juicer-Tools-Quick-Start) [Pre](Pre)** creates [hic files](Data) from aligned Hi-C reads (i.e., lists of Hi-C contacts).

Follow the links below to get started:

* [Installation](Installation)
  * [Dependencies](Installation#dependencies)
  * [Directory Structure](Installation#directory-structure)
* [Running Juicer](Running-Juicer-on-a-cluster)
* [Detailed usage](Usage)