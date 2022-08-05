# Quick Description

HOTSPOT is an algorithm for differential feature calling. It accepts a list of Hi-C maps and returns a list of differential feature locations in bedpe format [[add link to bedpe format page here]]. 

- This algorithm utilizes absolute cut-offs for filtering out signals that don't seem to be differential features, and it uses the 'Percent Contact' [[add link to percent contact metric page here]] metric for absolute comparison of signals across maps. 

This is the usage that most users will likely use (more detailed usage below):
	hotspot [--res resolution] [--norm normalization] <HiC files> <outputFileName>
Upon a successful run of HOTSPOT, by default, '.hotspot.bedpe' will be suffixed to the output file name, meaning it will be created as such:
	.../outputFileName.hotspot.bedpe

# Examples

NOTE: HOTSPOT will choose the default value for resolution (10000) and normalization type (SCALE) for HiC files if no specifications are given

	hotspot local/folder/HIC006.hic,local/folder/HIC007.hic,local/folder/HIC008.hic local/folder/output

This command will run HOTSPOT at 10kB (default) resolution with the normalization type SCALE (default) across HIC006, HIC007, HIC008 and save the locations of differential features in the output.hotspot.bedpe file.

	hotspot --res 10000 --norm VC https://s3.us-central-1.wasabisys.com/aiden-encode-hic-mirror/mapq30/S1_w71_kidney.hic,https://s3.us-central-1.wasabisys.com/aiden-encode-hic-mirror/mapq30/S3_w73_ratrium.hic,https://s3.us-central-1.wasabisys.com/aiden-encode-hic-mirror/mapq30/S1_uw40_rvent.hic,https://s3.us-central-1.wasabisys.com/aiden-encode-hic-mirror/mapq30/S4_w62_pancreas.hic 4tissues

This command will run HOTSPOT at 10kB resolution with the normalization type VC on mirror Hi-C maps for kidney, right atrium, right ventricle, and pancreas and save the locations of differential features in the 4tissues.hotspot.bedpe file.

# Detailed Usage

	hotspot hotspot [--res resolution] [--norm normalization (NONE/VC/VC_SQRT/KR/SCALE)] <HiC files> <outputFileName>

The required arguments are: 
* <HiC files>: Addresses of HiC files which should end with ".hic". These are the files for Hi-C maps that get compared to determine differential features. URLs or local addresses may be used. NOTE that files must be separated with a comma and no white spaces should be omitted between files.
* <outputFileName>: Name for the bedpe file that will be created (or written into) by HOTSPOT. Can be visualized directly in Juicebox using the "Load Tracks" -> "Local File" option. This file can also be converted into a URL and loaded as a track that way. NOTE: ".hotspot.bedpe" will be suffixed at the end of the file name when the file is created. **IMPORTANT:** the ideal resolution for HOTSPOT to be used is 10kB. Other resolutions being used will likely result in suboptimal results such as excessive noise. 
The optional arguments are:
* `--res <int>` Resolution for which HOTSPOT will be run. Note that this integer is understood in base pair units (not kB, mB, etc.)
* `--norm <NONE/SCALE/VC/VC_SQRT/KR>` Normalizations (case sensitive) that can be selected. Generally, SCALE balancing should be used when available.

# Defaults

These are the default parameters in for HOTSPOT described with all the available flags.

	--res 10000
	--norm SCALE
