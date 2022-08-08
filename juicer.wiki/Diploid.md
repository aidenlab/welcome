# Creating Diploid Hi-C Maps #

To create a diploid Hi-C map, you must have a phased [VCF file](http://www.internationalgenome.org/wiki/Analysis/Variant%20Call%20Format/vcf-variant-call-format-version-40/) and the [merged_nodups.txt](https://github.com/theaidenlab/juicer/wiki/Pre#long-format) file from running Juicer.  

The diploid script is implemented for [UGER](https://github.com/theaidenlab/juicer/blob/master/UGER/scripts/diploid.sh) and for [CPU](https://github.com/theaidenlab/juicer/blob/master/CPU/common/diploid.sh).

```
Usage: diploid.sh -g genomeID -s stem_or_vcf [-h]
       genomeID must be defined in the script, e.g. "hg19" or "mm10";
       alternatively, it can be the chrom.sizes file
       stem must be the stem where the chr_pos and paternal_maternal files are;
       alternatively, the full path to the phased vcf"
```

Run the script from the directory containing "merged_nodups.txt"

For each read pair in "merged_nodups.txt" in which at least one read end overlaps a SNP and the minimum MAPQ is 10, the script will print out to the file "diploid.txt" the read information plus additional strings indicating the position and nucleotide at the SNPs.

This file is then automatically parsed by the script to create hic files for each parent.  

The table below describes the output after running diploid.

| File | Description |
| --- | --- |
| diploid.txt | Hi-C contacts in which at least one read end overlaps at least one SNP, with said SNP information appended |
| maternal.hic | Hi-C contacts maps for the maternal chromosomes |
| paternal.hic | Hi-C contact maps for the paternal chromosomes |
| maternal_both.txt | Subset of diploid.txt in which both read ends have SNPs and are maternal |
| paternal_both.txt | Subset of diploid.txt in which both read ends have SNPs and are paternal |
| maternal.txt | Subset of diploid.txt in which one (and only one) read end has SNPs and is maternal; other end is indeterminate |
| paternal.txt | Subset of diploid.txt in which one (and only one) read end has SNPs and is paternal; other end is indeterminate |
| diff.txt | Subset of diploid.txt in which one read end is maternal and the other is paternal |
| mismatch.txt | Subset of diploid.txt in which at least one of two conditions has occurred: 1) at least one SNP did not match maternal or paternal (reference or alternate); 2) on the same read end, SNPs are not consistent between maternal and paternal |

Additionally, running diploid for the first time will produce chr_pos and maternal_paternal text files from the VCF files. If you want to run subsequent experiments against the same phasing information, you can just send in the stem of these files instead of reprocessing the VCF.

# Troubleshooting #
Statistics can be calculated by counting the number of lines in the subset files. A large number of mismatches could indicate a problem with your assembly or phasing; we found a big difference depending on the initial VCF (see Rao & Huntley et al., Cell 2014).  A large diff rate would indicate many interchromosomal interactions, which is usually not expected. A very skewed maternal/paternal read ratio can indicate mapping issues.