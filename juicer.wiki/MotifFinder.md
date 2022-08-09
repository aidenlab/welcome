# Finding DNA Motifs for Loops (MotifFinder)
## Usage ##
```
motifs <genomeID> <bed_file_dir> <looplist> [custom_global_motif_list]
```

The required arguments are: 

* &lt;genomeID>: Example hg19 or hg38
* &lt;bed_file_dir> File path to a directory which contains two folders: "unique" and "inferred". These folders should contain a combination of RAD21, SMC3, and CTCF ChIP-Seq tracks (.bed files). By intersecting these 1D tracks, the strongest peaks will be identified. The "unique" folder should generally contain a more stringent combination of BED files than the "inferred" folder. For instance, the "unique" folder could contain a CTCF track generated by the intersection of several CTCF bed files, in conjunction with RAD21 and SMC3. The "inferred" folder may just contain a CTCF track. If only CTCF data is available, use the same ChIP-Seq peaks in both the "unique" and "inferred" folders.
* &lt;looplist>: List of peaks in standard 2D feature format (chr1 x1 x2 chr2 y1 y2 color ...)


Optional arguments:
* [custom_global_motif_list]: Motif list output using FIMO format (by default, Juicer will attempt to find the file from an online repository). Genomewide [FIMO](http://meme-suite.org/doc/fimo.html) motifs are available on [Box](https://bcm.app.box.com/v/juicerawsmirror) under `/opt/juicer/references/genomewide_ctcf_motif_fimo`.

## Examples ##
See this Colab notebook with an example run: [notebook](https://colab.research.google.com/drive/1ucttsmbfJ7_HVw3VkWPSy-xqNKYF_VDh?usp=sharing)

Assuming the following file structure is present:

```
/path/to/local/bed/files/unique/CTCF.bed
/path/to/local/bed/files/unique/RAD21.bed
/path/to/local/bed/files/unique/SMC3.bed
/path/to/local/bed/files/inferred/CTCF.bed

motifs hg19 /path/to/local/bed/files gm12878_hiccups_loops.txt hg_19_custom_motif_list.txt
```
This command will find motifs from hg_19_custom_motif_list.txt for the loops in gm12878_hiccups_loops.txt and save them to gm12878_hiccups_loops_with_motifs.txt. The CTCF, RAD21, and SMC3 BED files will be used together (i.e. intersected) to find unique motifs. Just the CTCF track will be used to infer best motifs.


Assuming the following file structure is present:

```
/path/to/local/bed/files2/unique/CTCF.bed
/path/to/local/bed/files2/inferred/CTCF.bed

motifs hg19 /path/to/local/bed/files2 gm12878_hiccups_loops.txt
```
This command will use default motifs for hg19/hg38/mm9/mm10 for the loops in gm12878_hiccups_loops.txt and save them to gm12878_hiccups_loops_with_motifs.txt. The CTCF BED file will be used to find unique and inferred motifs.

## Result ##

Motif Finder will create a new file looplist_with_motifs.txt, which will add 10 fields for each loop in the loop list. See original loop list fields [here](HiCCUPS#loop-list-content).

The additional fields use the following format:
```
motif_x1    motif_x2    sequence1    orientation1    uniqueness1    
		motif_y1    motif_y2    sequence2    orientation2    uniqueness2
```

Explanations of each field are as follows:
* motif_x1,x2 = the start and end coordinates of the localized CTCF motif within the upstream loop anchor
* sequence1 = the sequence of the localized CTCF motif within the upstream loop anchor
* orientation1 = the orientation of the localized CTCF motif within the upstream loop anchor; p’ if the motif sequence is on the forward strand and ’n’ if the motif sequence is on the reverse strand
* uniqueness1 = whether the localized CTCF motif within the upstream loop anchor was uniquely called (‘u’) or inferred based on the convergent orientation principle (‘i’)
* motif_y1,y2; sequence2; orientation2; and uniqueness2 are the same as above except for the downstream loop anchor.

If the fields are ‘NA’ that indicates that we were unable to localize the anchor to a single CTCF motif.

See Section VI.e.7 of the Extended Experimental Procedures of <a href="http://www.cell.com/cell/abstract/S0092-8674(14)01497-4">Rao, Huntley et al. Cell 2014</a> for more details.