Juicer is designed to be run on a cluster system. We have created versions of
Juicer that run on [Univa](https://github.com/theaidenlab/juicer/tree/master/UGER), [SLURM](https://github.com/theaidenlab/juicer/tree/master/SLURM), and 
[LSF](https://github.com/theaidenlab/juicer/tree/master/LSF). If you'd like to run in the cloud, please see our [AWS](Running-Juicer-on-Amazon-Web-Services) directions to get started. 

The below directions apply to all systems, including the [single node](https://github.com/theaidenlab/juicer/tree/master/CPU) version.

1. Choose your cluster system or single CPU. Juicer is currently available in the cloud on [AWS](Running-Juicer-on-Amazon-Web-Services), on [LSF](https://github.com/theaidenlab/juicer/tree/master/LSF), [Univa](https://github.com/theaidenlab/juicer/tree/master/UGER), or [SLURM](https://github.com/theaidenlab/juicer/tree/master/SLURM), or on a single [CPU](https://github.com/theaidenlab/juicer/tree/master/CPU)

2. Follow the instructions in the [Installation](Installation) section.  Be sure you know how to load the required software on your system; cluster systems might have slightly different names, and you might need to change the master "juicer.sh" script to reflect this.

3. Log into your cluster

4. Install the appropriate Juicer scripts for your system in a directory; we will assume this directory is `/home/user/juicedir`. For example, if you were using SLURM, you would copy the folder `scripts` underneath [SLURM](https://github.com/theaidenlab/juicer/tree/master/SLURM) to `/home/user/juicedir/scripts`

5. Under `/home/user/juicedir`, there should be a folder `references` that contains the reference fasta file for your genome
and the BWA index files. You can soft-link if necessary, or otherwise download the fasta files from [UCSC](http://genome.ucsc.edu/) and run `bwa index` on the fasta file.

6. Under `/home/user/juicedir`, you should also create a folder `restriction_sites`. This should contain your [restriction site file](File-formats). You can create this file using the [generate_site_positions.py](https://github.com/theaidenlab/juicer/blob/master/misc/generate_site_positions.py) Python script, or download already created ones from [the Juicer AWS mirror](https://bcm.box.com/v/juicerawsmirror). 

7. [Optional, only for deep maps] Create the bedfile folder under `/home/user/juicedir/references/motif` and underneath that, two folders: "unique" and "inferred". These folders should contain a combination of RAD21, SMC3, and CTCF BED files. 

8. Create a custom directory (e.g. mkdir -p /custom/filepath/MyHIC)

9. Download the test data.
   * Option 1: To see how Juicer runs on a deep sequencing test data set, download the following, consisting of chromosome19 from the Cell 2014 in-situ combined GM12878 map: 
      * [chr19_R1.fastq.gz](http://juicerawsmirror.s3.amazonaws.com/opt/juicer/work/MBR19/fastq/chr19_R1.fastq.gz) 
      * [chr19_R2.fastq.gz](http://juicerawsmirror.s3.amazonaws.com/opt/juicer/work/MBR19/fastq/chr19_R2.fastq.gz)
   * Option 2: To run Juicer on a small test data set, download the following MiSeq GM12878 in-situ files:
      * [HIC003_R1.fastq.gz](http://juicerawsmirror.s3.amazonaws.com/opt/juicer/work/HIC003/fastq/HIC003_S2_L001_R1_001.fastq.gz) 
      * [HIC003_R2.fastq.gz](http://juicerawsmirror.s3.amazonaws.com/opt/juicer/work/HIC003/fastq/HIC003_S2_L001_R2_001.fastq.gz)

10. Create a fastq directory under the top directory (e.g.  `cd /custom/filepath/MyHIC; mkdir fastq`).  Soft-link or copy your fastq files (zipped or unzipped) to that directory

11. Type `screen` then launch Juicer:
    ```
    /home/user/juicedir/scripts/juicer.sh [options]
    ```
    Running without any options will default to the genome of hg19 and the restriction site of MboI. See [Usage](Usage) for more options; to adjust genome and/or site, use `-g <genomeID>` and `-s <restriction_site>`. 

    The files will be split if necessary and Juicer will launch.  

12.  Sample output; the "exit code 0" statement means that the split successfully completed.
     ```
     (-: Looking for fastq files...fastq files exist

     Prepending: UGER (already loaded)

     (-: Aligning files matching HIC001/fastq/_R.fastq in queue short to genome hg19

     (-: Created HIC001/splits and HIC001/aligned. Splitting files

     Your job 95416 ("a1439405283split0") has been submitted

     Job 95416 exited with exit code 0.

     Your job 95419 ("a1439405283split1") has been submitted

     Job 95419 exited with exit code 0.

     (-: Starting job to launch other jobs once splitting is complete

     Your job 95421 ("a1439405283_001000.fastqcountligations") has been submitted

     Your job 95422 ("a1439405283_align1_001000.fastq") has been submitted

     Your job 95423 ("a1439405283_align2_001000.fastq") has been submitted

     Your job 95424 ("a1439405283_merge_001000.fastq") has been submitted

     Your job 95425 ("a1439405283_fragmerge") has been submitted

     Your job 95426 ("a1439405283_osplit") has been submitted

     Your job 95427 ("a1439405283_finallaunch") has been submitted

     Your job 95428 ("a1439405283_done") has been submitted

     (-: Finished adding all jobs... please wait while processing.

     ```
13. Check out the results with the appropriate command in your cluster; `bjobs` for LSF and AWS, `squeue` for SLURM, `qstat` for Univa. The single CPU script will run until it finishes or exits.

14. If there are no jobs left, type `cat debug/finalcheck*`; you should see a "Pipeline successfully completed" message. For some clusters, there might be only one file, e.g. `lsf.out` or `uger.out`; in this case, type `tail lsf.out` to see the message.

15. Results are available in the aligned directory. The Hi-C maps are in inter.hic (for MAPQ > 0) and inter_30.hic (for MAPQ >= 30). The Hi-C maps can be loaded in [Juicebox](https://github.com/theaidenlab/juicebox/wiki) and explored. They can also be used for [feature annotation and analysis](Feature-Annotation) and to [extract matrices](Data-Extraction) at specific resolutions. You can also directly manipulate them with the [Straw API](https://github.com/theaidenlab/straw/wiki)

16. These results also include automatic feature annotation. The output files include a genome-wide annotation of loops and, whenever possible, the CTCF motifs that anchor them (identified using the [HiCCUPS](HiCCUPS) algorithm). The files also include a genome-wide annotation of contact domains (identified using the [Arrowhead](Arrowhead) algorithm). The formats of these files are described in the [Juicebox](https://github.com/theaidenlab/juicebox/wiki/Annotations) tutorial online; both files can be loaded into Juicebox as a 2D annotation.

17.  When the pipeline has completed successfully, you will see the folders `aligned`, `debug`, and `splits`.  The `debug` folder contains logging information for the pipeline.  The `splits` folder is a temporary working directory and can be deleted once you are sure the pipeline ran successfully.  The `aligned` folder contains the results:
     * **inter.hic / inter_30.hic**: The .hic files for Hi-C contacts at MAPQ > 0 and at MAPQ >= 30, respectively
     * **merged_nodups.txt**: The Hi-C contacts with duplicates removed. This file is also input to the assembly and diploid pipelines
     * **collisions.txt**: Reads that map to more than two places in the genome
     * **inter.txt, inter_hists.m / inter_30.txt, inter_30_hists.m**: The statistics and graphs files for Hi-C contacts at MAPQ > 0 and at MAPQ >= 30, respectively.  These are also stored within the respective .hic files in the header.  The .m files can be loaded into Matlab.  The statistics and graphs are displayed under Dataset Metrics when loaded into Juicebox
     * **dups.txt, opt_dups.txt**: Duplicates and optical duplicates
     * **abnormal.sam, unmapped.sam**: Abnormal chimeric and unmapped reads 
     * **merged_sort.txt**: This is a combination of merged_nodups / dups / opt_dups and can be deleted once the pipeline has successfully completed
     * **stats_dups.txt / stats_dups_hists.m**: Statistics and graphs on the duplicates  

You should run the script `cleanup.sh` to zip all the text files and delete the unnecessary `splits` directory and `merged_sort.txt` file once you are sure the pipeline has successfully completed.


