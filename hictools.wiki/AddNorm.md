## `Add Norm`

Juicer automatically calls addNorm as a part of <a href="https://github.com/aidenlab/juicer/wiki/Pre">Pre</a>. In case you have specifically not calculated norms by using the `-n` flag when calling <a href="https://github.com/aidenlab/juicer/wiki/Pre">Pre</a>, you may use the addNorm method to normalize. Additionally, you can submit your own vectors to be stored with the hic file. Multiple normalization vectors can be added in this manner; they will appear in the dropdown menu in using the names assigned in the file you provide.

If you create a .hic file without normalization vectors (using the `-n` flag) or if you want to apply genome-wide normalization or not normalize the fragment matrices, you can use the `addNorm` command. This will add all normalization vectors (coverage, square root coverage, and balanced)
```
  addNorm [-w genome-wide-resolution] [-F] [-k normalizations] <input_HiC_file> 
```
Flags:
* `<input_HiC_file>`: File to normalize; this will delete any previous normalizations
Optional:
* `-w <genome-wide resolution>`: Smallest resolution to calculate genome-wide resolution; e.g., if 7000, genome-wide normalizations will be calculated for 2.5Mb, 1Mb, 500Kb, 250Kb, 100Kb, 50Kb, 25Kb, and 10Kb but not for 5Kb. Note that genome-wide resolution can be very expensive in terms of memory; this flags allows for a memory/normalization trade-off.
If not set or set to 0, no genome-wide resolutions will be calculated
* `-F`: Do not calculate normalizations for fragment-delimited matrices

As of version 1.14.07:
* `-k <comma-separated list of normalizations>` calculate specific normalizations (including genomewide normalizations, e.g. `GW_KR`); Full list of built-in normalizations is `VC, VC_SQRT, KR,SCALE, GW_KR, GW_SCALE, GW_VC, INTER_KR, INTER_SCALE, INTER_VC` [default: `VC,VC_SQRT,KR,SCALE`]

----

## `Add additional vectors as the norm or scaling target (BETA)`
We allow the ability to send in a text file that contains an additional pre-calculated normalization vector. Multiple such vectors can be specified in the same text file and built into the hic file. They will appear in the normalization drop down menu using the names provided in the text file. Prior loaded normalization vectors are not deleted and will be preserved.

Furthermore, you may provide a target coverage vector to which the map is to be scaled to. To do so, use the `vector_scale` header rather than the `vector` header in the provided text file. Multiple such vectors can be provided in the same text file as long as the appropriate headers (`vector` and `vector_scale`) are used for each chromosome-resolution and normalization/target.

----
## `Usage`
```
  addNorm <input_HiC_file> <input_normalization_vector>
```

----
## `File format for normalization vector`
The file format for the normalization vector is a simple text file. For each new chromosome-resolution combination, there should be a new header line starting with the word `vector` or `vector_scale`. Then comes the name of the normalization, the chromosome, and the resolution.

For example:
```
vector  MyNewNorm  chr1    2500000 BP
0.317522718673
0.72654265741
0.29353335424
0.638594927778
0.778175426373
0.322731736798
.
0.866251628293
0.170958650245
0.33980309017
0.968321393859
0.20895742749
.
vector_scale  MySecondNorm  chr2    2500000 BP
0.373096503455
0.352043644426
0.482002469483
0.222967309304
0.35294886705
0.732542404884
0.859455987572
0.696335078534
0.033424729077
0.743690271992
0.012562851558
0.179414542021
```
There should be the same number of entries in the norm vector as the size of the chromosome divided by the bin size while rounding up. E.g. for chromosome 1 in hg19 with 10K resolution, there should be ceil(249250621/10000) entries (so 24926). 