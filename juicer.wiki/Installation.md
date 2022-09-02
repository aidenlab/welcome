# Installation

----

## `Dependencies`
* For alignment and creation of the Hi-C pairs file `merged_nodups.txt`:
   * [GNU CoreUtils](https://www.gnu.org/software/coreutils/manual/)
   * [Burrows-Wheeler Aligner (BWA)](http://bio-bwa.sourceforge.net/)
* For .hic file creation and [Juicer tools analysis](https://github.com/theaidenlab/juicer/wiki/Feature-Annotation): 
   * [Java 1.7 or 1.8 JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html). 
([Alternative link](http://tecadmin.net/install-oracle-java-8-jdk-8-ubuntu-via-ppa/) for Ubuntu/LinuxMint).  Minimum system requirements for running Java can be found at http://java.com/en/download/help/sysreq.xml
   * [Latest Juicer Tools jar](https://github.com/theaidenlab/juicer/wiki/Download)
* For peak calling:
   * [CUDA](https://developer.nvidia.com/cuda-downloads) and an NVIDIA GPU
   * The native libraries included with Juicer are compiled for CUDA 7. Other versions of CUDA can be used, but you will need to download the respective native libraries from [JCuda](http://www.jcuda.org/downloads/downloads.html).
   * For best performance, use a dedicated GPU. You may also be able to obtain access to GPU clusters through Amazon Web Services or a local research institution.
1. Verify that you've installed all [dependencies](#dependencies).
2. Set up your [directories](#directory-structure). You should have a Juicer directory containing `scripts/`, `references/`, and optionally `restriction_sites/`, and a different working directory containing `fastq/`. You should download
the [Juicer tools jar](Download) and install it in your `scripts/` directory.
3. Run [Juicer](Usage).

## `Example with CPU version ` 
  ```bash
  git clone https://github.com/theaidenlab/juicer.git
  cd <myJuicerDir>
  ln -s ~/juicer/CPU scripts
  cd scripts/common
  wget https://hicfiles.tc4ga.com/public/juicer/juicer_tools.1.9.9_jcuda.0.8.jar
  ln -s juicer_tools.1.9.9_jcuda.0.8.jar  juicer_tools.jar
  cd ../..
  mkdir references
  cp <my_reference_fastas_and_indices> references/
  # this is optional, only needed for fragment-delimited files
  ln -s <myRestrictionSiteDir> restriction_sites
  cd <myWorkingDir>
  mkdir fastq
  mv <fastq_files> fastq/
  <myJuicerDir>/scripts/juicer.sh -D <myJuicerDir> 
```
`<myJuicerDir>` is where ever you want to store the Git repository (keeping in mind you will want to pull updates).  `<my_reference_fastas_and_indices>` is your reference assembly and the BWA index files. `<myRestrictionSiteDir>` will contain the restriction site files, see below for more information.  `<fastq_files>` are your sequenced reads; they can remain gzipped.

----
## `Example with cluster version and downloading reference files`
```
cd /home
mkdir references; cd references
wget https://s3.amazonaws.com/juicerawsmirror/opt/juicer/references/Homo_sapiens_assembly19.fasta
wget https://s3.amazonaws.com/juicerawsmirror/opt/juicer/references/Homo_sapiens_assembly19.fasta.amb
wget https://s3.amazonaws.com/juicerawsmirror/opt/juicer/references/Homo_sapiens_assembly19.fasta.ann
wget https://s3.amazonaws.com/juicerawsmirror/opt/juicer/references/Homo_sapiens_assembly19.fasta.bwt
wget https://s3.amazonaws.com/juicerawsmirror/opt/juicer/references/Homo_sapiens_assembly19.fasta.pac
wget https://s3.amazonaws.com/juicerawsmirror/opt/juicer/references/Homo_sapiens_assembly19.fasta.sa
mkdir ../restriction_sites; cd ../restriction_sites
wget https://s3.amazonaws.com/juicerawsmirror/opt/juicer/restriction_sites/hg19_MboI.txt
cd ..
git clone https://github.com/theaidenlab/juicer.git
ln -s juicer/SLURM/scripts/ scripts
cd scripts
wget https://hicfiles.tc4ga.com/public/juicer/juicer_tools.1.9.9_jcuda.0.8.jar
ln -s juicer_tools.1.7.6_jcuda.0.8.jar juicer_tools.jar
cd ..
mkdir HIC003; cd HIC003
mkdir fastq; cd fastq
wget http://juicerawsmirror.s3.amazonaws.com/opt/juicer/work/HIC003/fastq/HIC003_S2_L001_R1_001.fastq.gz
wget http://juicerawsmirror.s3.amazonaws.com/opt/juicer/work/HIC003/fastq/HIC003_S2_L001_R2_001.fastq.gz
cd ..
/home/scripts/juicer.sh -D /home
```
### Test data
Test data can be found here:
* MiSeq GM12878 in-situ files:
    * [HIC003_R1.fastq.gz](http://juicerawsmirror.s3.amazonaws.com/opt/juicer/work/HIC003/fastq/HIC003_S2_L001_R1_001.fastq.gz)
    * [HIC003_R2.fastq.gz](http://juicerawsmirror.s3.amazonaws.com/opt/juicer/work/HIC003/fastq/HIC003_S2_L001_R2_001.fastq.gz)
* Chromosome 19 from the Cell 2014 in-situ combined GM12878 map (deep enough for domains and loops): 
   * [chr19_R1.fastq.gz](http://juicerawsmirror.s3.amazonaws.com/opt/juicer/work/MBR19/fastq/chr19_R1.fastq.gz) 
   * [chr19_R2.fastq.gz](http://juicerawsmirror.s3.amazonaws.com/opt/juicer/work/MBR19/fastq/chr19_R2.fastq.gz)



# Cluster Specification #
Juicer currently works with the following resource management software:
* [OpenLava](http://www.openlava.org/)
* [LSF](http://www-03.ibm.com/systems/services/platformcomputing/lsf.html)
* [SLURM](http://slurm.schedmd.com/download.html)
* GridEngine ([Univa](http://www.univa.com/), etc. any flavor)

Make sure to copy the appropriate scripts from the github repo to your cluster or laptop, as well as the fastq reads and appropriate reference files.  You should download the [Juicer tools jar](Download) and install it in your `scripts/` directory.

# Directory Structure #
See the [Box mirror](https://bcm.box.com/v/juicerawsmirror) for an easy-to-navigate view of the directory structure. 

The following also shows a sample configuration of the all the files and directories on the cluster once Juicer is fully set up. It assumes that all files needed by Juicer are created under `/opt/juicer`. 

You can also access another public mirror of these files by going to `https://s3.amazonaws.com/juicerawsmirror/opt/juicer/[paths_below]`, for example: https://s3.amazonaws.com/juicerawsmirror/opt/juicer/work/HIC003/fastq/HIC003_S2_L001_R1_001.fastq.gz.
```
# tmp directory
/opt/juicer/tmp

# sample work directory is /opt/juicer/work/HIC003
/opt/juicer/work/HIC003/fastq
/opt/juicer/work/HIC003/fastq/HIC003_S2_L001_R1_001.fastq.gz
/opt/juicer/work/HIC003/fastq/HIC003_S2_L001_R2_001.fastq.gz

# another sample work directory is /opt/juicer/work/MBR19
/opt/juicer/work/MBR19/fastq
/opt/juicer/work/MBR19/fastq/chr19_R1.fastq.gz
/opt/juicer/work/MBR19/fastq/chr19_R2.fastq.gz

# Core Juicer scripts from github in /opt/juicer/scripts
/opt/juicer/scripts/chimeric_blacklist.awk
/opt/juicer/scripts/statistics.pl
/opt/juicer/scripts/stats_sub.awk
/opt/juicer/scripts/split_rmdups.awk
/opt/juicer/scripts/countligations.sh
/opt/juicer/scripts/juicer_tools
/opt/juicer/scripts/juicer_tools.jar
/opt/juicer/scripts/juicer_postprocessing.sh
/opt/juicer/scripts/dups.awk
/opt/juicer/scripts/juicer.sh
/opt/juicer/scripts/LibraryComplexity.class
/opt/juicer/scripts/hicInternalMenu.properties
/opt/juicer/scripts/abnormal.awk
/opt/juicer/scripts/check.sh
/opt/juicer/scripts/fragment.pl
/opt/juicer/scripts/makemega_addstats.awk
/opt/juicer/scripts/mega.sh
/opt/juicer/scripts/relaunch_prep.sh
/opt/juicer/scripts/cleanup.sh

# Sequence reference files in /opt/juicer/references
# hg19 and mm9 reference files in mirror
/opt/juicer/references/Homo_sapiens_assembly19.fasta
/opt/juicer/references/Mus_musculus_assembly9_norandom.fasta
```

Make sure to copy the appropriate scripts from the github repo to your cluster as well as the fastq reads and appropriate reference files.

After running BWA indexing (might take a couple hours) `bwa index <fasta file>`:
```
# after running BWA indexing
/opt/juicer/references/Homo_sapiens_assembly19.fasta.sa
/opt/juicer/references/Homo_sapiens_assembly19.fasta.ann
/opt/juicer/references/Homo_sapiens_assembly19.fasta.amb
/opt/juicer/references/Homo_sapiens_assembly19.fasta.pac
/opt/juicer/references/Homo_sapiens_assembly19.fasta.bwt
/opt/juicer/references/Mus_musculus_assembly9_norandom.fasta.bwt
/opt/juicer/references/Mus_musculus_assembly9_norandom.fasta.amb
/opt/juicer/references/Mus_musculus_assembly9_norandom.fasta.pac
/opt/juicer/references/Mus_musculus_assembly9_norandom.fasta.ann
/opt/juicer/references/Mus_musculus_assembly9_norandom.fasta.sa
```
(OPTIONAL): After building the restriction sites files `python generate_site_positions.py <enzyme> <genome ID> <fasta>`
https://github.com/theaidenlab/juicer/blob/master/misc/generate_site_positions.py
(If you don't use fragment delimited resolutions, you must run Juicer with the `-x` flag)
```
# restriction sites files in /opt/juicer/restriction_sites
/opt/juicer/restriction_sites/mm9_HindIII.txt
/opt/juicer/restriction_sites/mm10_MboI.txt
/opt/juicer/restriction_sites/mm10_DpnII.txt
/opt/juicer/restriction_sites/hg19_MboI.txt
/opt/juicer/restriction_sites/hg38_MboI.txt
/opt/juicer/restriction_sites/hg38_DpnII.txt
/opt/juicer/restriction_sites/hg19_DpnII.txt
/opt/juicer/restriction_sites/hg19_HindIII.txt
/opt/juicer/restriction_sites/mm9_DpnII.txt
```
