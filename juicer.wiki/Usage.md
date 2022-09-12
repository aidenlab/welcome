## Juicer Usage
```bash
juicer.sh [-g genomeID] [-d topDir] [-q queue] [-l long queue] [-s site]
                 [-a about] [-S stage] [-p chrom.sizes path]
                 [-y restriction site file] [-z reference genome file]
                 [-C chunk size] [-D Juicer scripts directory]
                 [-Q queue time limit] [-L long queue time limit] [-b ligation] [-t threads]
                 [-A account name] [-e] [-h] [-f] [-j]
* [genomeID] must be defined in the script, e.g. "hg19" or "mm10" (default 
  "hg19"); alternatively, it can be defined using the -z command
* [topDir] is the top level directory (default pwd)
     [topDir]/fastq must contain the fastq files
     [topDir]/splits will be created to contain the temporary split files
     [topDir]/aligned will be created for the final alignment
* [queue] is the queue for running alignments (default "commons")
* [long queue] is the queue for running longer jobs such as the hic file
  creation (default "long")
* [site] must be defined in the script, e.g.  "HindIII" or "MboI" 
  (default "none")
* [about]: enter description of experiment, enclosed in single quotes
* [stage]: must be one of "chimeric", "merge", "dedup", "final", "postproc", or "early".
    -Use "merge" when alignment has finished but the merged_sort file has not
     yet been created.
    -Use "dedup" when the files have been merged into merged_sort but
     merged_nodups has not yet been created.
    -Use "final" when the reads have been deduped into merged_nodups but the
     final stats and hic files have not yet been created.
    -Use "postproc" when the hic files have been created and only
     postprocessing feature annotation remains to be completed.
    -Use "early" for an early exit, before the final creation of the hic files
    Can also use -e flag to exit early
* [chrom.sizes path]: enter path for chrom.sizes file
* [restriction site file]: enter path for restriction site file (locations of
  restriction sites in genome; can be generated with the script
  misc/generate_site_positions.py)
* [reference genome file]: enter path for reference sequence file, BWA index
  files must be in same directory
* [chunk size]: number of lines in split files, must be multiple of 4
  (default 90000000, which equals 22.5 million reads)
* [Juicer scripts directory]: set the Juicer directory,
  which should have scripts/ references/ and restriction_sites/ underneath it
  (default /gpfs0/juicer/)
* [queue time limit]: time limit for queue, i.e. -W 12:00 is 12 hours
  (default 2880)
* [long queue time limit]: time limit for long queue, i.e. -W 168:00 is one week
  (default 7200)
* [ligation junction]: use this string when counting ligation junctions
* [threads]: number of threads when running BWA alignment
* [account name]: user account name on cluster
* -e: Use for an early exit, before the final creation of the hic files
* -f: include fragment-delimited maps in hic file creation
* -h: print this help and exit
```												
* **Running Juicer** with no arguments will run it with genomeID hg19 and site none
* **Providing a genome ID**: if not defined in the script, you can either directly modify the script or provide the script with the files needed. You would provide the script with the files needed via "-z reference_sequence_path" (needs to have the BWA index files in same directory), "-p chrom_sizes_path" (these are the chromosomes you want included in .hic file), and "-s site_file" (this is the listing of all the restriction site locations, one line per chromosome). Note that ligation junction won't be defined in this case. The script (misc/generate_site_positions.py) can help you generate the file
* **Providing a restriction enzyme**: if not defined in the script, you can either directly modify the script or provide the files needed via the "-s site_file" flag, as above. Alternatively, if you don't want to do any fragment-level analysis (as with a DNAse experiment), you should assign the site "none", as in `juicer.sh -s none`.  You can also give an alternate ligation junction than the standard that would be derived from the site via the `-b` flag
* **Directory structure**: Juicer expects the fastq files to be stored in a directory underneath the top-level directory. E.g. HIC001/fastq. By default, the top-level directory is the directory where you are when you launch Juicer; you can change this via the -d flag. Fastqs can be zipped. [topDir]/splits will be created to contain the temporary split files and should be deleted once your run is completed. [topDir]/aligned will be created for the final files, including the hic files, the statistics, the valid pairs (merged_nodups), the collisions, and the feature annotations.
* **Queues** are complicated and it's likely that you'll have to modify the script for your system, though we did our best to avoid this. By default there's a short queue and a long queue. We also allow you to pass in wait times for those queues; this is currently ignored by the UGER and SLURM versions. The short queue should be able to complete alignment of one split file. The long queue is for jobs that we expect to take a while, like writing out the merged_sort file
* **Chunk size** is intimately associated with your queues; a smaller chunk size means more alignment jobs that complete in a faster time. If you have a hard limit on the number of jobs, you don't want too small of a chunk size. If your short queue has a very limited runtime ceiling, you don't want too big of a chunk size. Run time for alignment will also depend on the particulars of your cluster. We launch ~5 jobs per chunk. Chunk size must be a multiple of 4.
* **Relaunch** via the same script. Type juicer.sh [options] -S stage where "stage" is one of chimeric, merge, dedup, final, postproc, or early. "chimeric" is when alignment is done but not chimera read handling. See below for more information. "merge" is for when alignment has finished but merged_sort hasn't been created; "dedup" is for when merged_sort is there but not merged_nodups (this will relaunch all dedup jobs); "final" is for when merged_nodups is there and you want the stats and hic files; "postproc" is for when you have the hic files and just want feature annotations; and "early" is for early exit, before hic file creation. You can also assign early exit via the "-e" flag and start at one of the other stages. If your jobs failed at the alignment stage, run relaunch_prep.sh and then run juicer.sh.
* **Miscelleaneous** options include -a 'experiment description', which will add the experiment description to the statistics file and the meta data in the hic file; -f for including fragment maps in the Hi-C file creation; and -D [Juicer scripts directory], to set an alternative Juicer directory; must have scripts/, references/, and restriction_sites/ underneath it

----
## Adding a new genome
To add a new genome to Juicer, follow these steps:

1. Download genome fasta file, put in references folder
2. Run `bwa index` on the fasta file
3. At the same time, run [generate_site_positions.py](https://github.com/theaidenlab/juicer/blob/master/misc/generate_site_positions.py) on the fasta file + your restriction enzyme (see [this site about the restriction site file format](https://github.com/theaidenlab/juicer/wiki/Pre#restriction-site-file-format))
4. Once generate_site_positions is done, run `awk 'BEGIN{OFS="\t"}{print $1, $NF}' mygenome_myenzyme.txt > mygenome.chrom.sizes` (where mygenome is your genome, like hg19, and myenzyme is your enzyme, like MboI)
5. Run juicer.sh with the flags `-z <path to genome fasta file>`, `-p <path to mygenome.chrom.sizes>`, and  `-y <path to  mygenome_myenzyme.txt>`

----
## Creating a "mega" map
To create statistics and a hic file from a series of replicates, you can use the `mega.sh` script.

Create the following directory structure (the files can be soft-linked):

```
/opt/juicer/work/HeLa/HIC001/aligned/merged_nodups.txt
/opt/juicer/work/HeLa/HIC002/aligned/merged_nodups.txt
/opt/juicer/work/HeLa/HIC003/aligned/merged_nodups.txt

/opt/juicer/work/HeLa/HIC001/aligned/inter.txt
/opt/juicer/work/HeLa/HIC002/aligned/inter.txt
/opt/juicer/work/HeLa/HIC003/aligned/inter.txt
```

Type
```
cd /opt/juicer/work/HeLa/
```
And then run mega.sh with the same kinds of flags as with Juicer:

```
/opt/juicer/scripts/mega.sh -g hg19 -s DpnII
```
A "mega" folder will be created at `/opt/juicer/work/HeLa/mega` and underneath that, the `aligned` folder will contain the results.

----
## Running on already aligned files
	
* Make top directory, fastq, splits: `mkdir experiment; cd experiment; mkdir fastq; mkdir splits`
* Put in splits folder with <filename1>.fastq.sam, filename2.fastq.sam, etc. For bams, use samtools view to write to sam
* Touch files in fastq directory with corresponding names: `cd fastq/; touch filename1_R1.fastq; touch filename1_R2.fastq; touch filename2_R1.fastq; touch filename2_R2.fastq`
* Link to these from splits: `cd ../splits; ln -s ../fastq/* .`
* Run with -S chimeric from top directory and whatever your flags are: `juicer.sh -S chimeric [other flags]`

----

## `Fastq` files
These are the raw data files that come off the sequencer. They include the read name, the read (a string of A,C,T,G, or N) and base quality information. See [this article](https://en.wikipedia.org/wiki/FASTQ_format) for more information. Juicer takes `.fastq` files and transforms them into contact matrices stored in a `.hic` file. 

