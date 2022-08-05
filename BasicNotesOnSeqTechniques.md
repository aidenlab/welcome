# Basic Notes on RNA-Seq, ChIP-Seq, ATAC-Seq,

Notes taken by: Michael Ngo

## RNA-Seq

[https://www.youtube.com/watch?v=tlf6wYJrwKY](https://www.youtube.com/watch?v=tlf6wYJrwKY)

- Goal: **measures differences in gene expression** (to know what genetic mechanism is causing the difference)
- **High throughput sequencing tells us which genes are active, and how much they are transcribed**
- 3 main steps in RNA-seq
    1. prepare a sequencing library
    2. sequence
        1. **TL;DR of steps: extract mRNA, sequence fragments, align the reads with a genome, and we count the reads per genes (and normalize)**
    3. data analysis
        1. PCA plots reduce the number of axes needed to present data. Most important differences are on the x-axis
            1. plotting data tells us if we can expect to find interesting differences and if we should excluse some samples from any down stream analysis
        2. identify differentially expressed genes between samples

## ChIP-Seq

[https://www.youtube.com/watch?v=nkWGmaYRues](https://www.youtube.com/watch?v=nkWGmaYRues)

- “**Ch**romatin **I**mmuno**p**recipitation combined with high-throughput **seq**uencing”
    - **Identifies the locations in the genome bound by proteins**
- DNA wraps around histones to “package DNA” and the packaging can regulate gene transcription (histones, depending on how they’re modified, can activate or repress genes)
- Process of ChIP-seq
    - glue proteins to DNA, cut up DNA, bind proteins of interest with antibodies, isolate antibodies, unglue and wash away proteins
    - Then, sequencing process is very similar to RNA-seq
    - we ultimately get a long list of genomic coordinates for all the reads and form a ChIP-seq track (basically a long bargraph that resembles audio tracks) and compare it to a control track. Statistically significant peaks are used to compare to different cell types, or look for binding motifs for specific proteins, or use its position to see if it seems to have an effect on genes

## ATAC-Seq

[https://www.youtube.com/watch?v=5HfNP-VVJWU](https://www.youtube.com/watch?v=5HfNP-VVJWU)

- Assay for Transposase-Accessible Chromatin, using sequencing
- method to **assess genome-wide chromatin accessibility**
- help: uncover how chromatin packaging and other factors affect gene expression
- Importance:
    - prior knowledge of regulatory elements not required (makes it powerful epigenetic discovery tool)
    - better alternative to understand chromatin accessibility, transcription factor binding, gene regulation in complex diseases, embryonic development, T-cell activation, and cancer
    - can be performed on bulk cell populations and single cells
    
- a nucleosome is DNA wrapped around a histone. Because the DNA in a nucleosome is tightly packed, it is considered mostly **inactive** because the **nucleosome limits accessibility** (for transcription)
- basically works by fragmenting off only the accessible portions of DNA and sequencing those
- “one of the 4 classes of methods used for assessing the status of the epigenome through analysis of chromatin accessability” (the other 3 techniques are DNase-seq, FAIRE-seq, and MNase-seq)
    - from [https://en.wikipedia.org/wiki/MNase-seq](https://en.wikipedia.org/wiki/MNase-seq)

## DNase-Seq

[https://www.youtube.com/watch?v=4VE44dAOe-g](https://www.youtube.com/watch?v=4VE44dAOe-g)

- DNase-Seq is used to **find chromatin accessibility and DNA regulatory regions**
- Maps out DNaseI hypersensitive regions of the genome that play an active role in transcription
    - correspond to open areas of chromatin (fewer histones) where gene regulatory regions are located (note: has a bias for proximal promoter regions, where a majority of transcription factors are known to bind)
    - has been shown to recover ~90% of known TF motifs (from ENCODE paper)



background info:

- with development, certain genes become more or less active. This is from proteins modifying histones or DNA.
    - There are also regulatory sequences of DNA that control gene expression (by binding to transcription factors). For transcription machinery to attach, that DNA must be accessible
- process uses the protein DNaseI enzyme that splices DNA at open areas of chromatin and preferentially cuts at sites where nearby there are specific (non-histone) proteins. High throughput sequencing used to determine those sits “hypersensitive” to DNaseI, corresponding to open chromatin
    - “**DNaseI hypersensitivity is the hallmark of regulatory DNA regions”**
        - from [https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3439153/](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3439153/)