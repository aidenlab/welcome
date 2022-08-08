# Juicebox #
<img src="https://github.com/theaidenlab/juicebox/wiki/images/graphic_juicebox.png" width="100%" alt="Overview">

Juicebox is visualization software for Hi-C experiments. Using Juicebox, you can
* visualize Hi-C maps by zooming in and out over many magnitudes of resolution in real time
* compare Hi-C maps with ENCODE tracks, genes, loops/domains, other Hi-C maps, & more
* explore a large archive of published Hi-C experiments
* load your own Hi-C data by creating your map using [Juicer tools](https://github.com/theaidenlab/juicer/wiki/Pre) and opening it in Juicebox
* ...and more!

# **NEW** [Juicebox and Juicebox.JS ENCODE tutorial](https://aidenlab.gitbook.io/juicebox/): [aidenlab.gitbook.io/juicebox](https://aidenlab.gitbook.io/juicebox/)

# Quick Start #



1. Start by downloading Juicebox for [Windows](https://s3.amazonaws.com/hicfiles.tc4ga.com/public/Juicebox.exe), [Mac](https://s3.amazonaws.com/hicfiles.tc4ga.com/public/Juicebox.dmg), or simply the [jar](https://s3.amazonaws.com/hicfiles.tc4ga.com/public/Juicebox.jar). Also available [here](Download).
2. Watch the video:

   <a href="http://www.youtube.com/watch?feature=player_embedded&v=xjNXyeUSfZM" target="_blank"><img src="http://img.youtube.com/vi/xjNXyeUSfZM/0.jpg" alt="Juicebox quick start video" width="400"  border="10" /></a>
3. Once you've successfully launched Juicebox, click File→Open to load a new Hi-C map. <img src="https://github.com/theaidenlab/juicebox/wiki/images/menu.png" alt="Menu" align=center>

   All of the Hi-C maps from our recent papers are available, as well as an archive of other published Hi-C experiments. Click Cell 2014→GM12878→in situ MboI→combined (4.9B) to open our largest map: the combined primary and replicate GM12878 library.

   <img src="https://github.com/theaidenlab/juicebox/wiki/images/allvsall.png" alt="All vs All">
4. Click on chromosome 17. This can be done either by selecting 17 x 17 below the Chromosome section on the toolbar and hitting the refresh button, or by clicking on chromosome 17 itself. Using the selector below Normalization, change the normalization to Balanced. Slide the resolution slider to 5 KB.
   
   <img src="https://github.com/theaidenlab/juicebox/wiki/images/juicebox3.png" alt="Chromosome 17">

5. Use your mouse to pan until your range is roughly 64,500 kb to 69,000 kb. Alternatively, in the Go panel, type 17:64500000-69000000 in both boxes and hit the refresh button. 

6. Now click Annotations in the menu bar and go to Load Basic Annotations. Select the Dataset Specific 2-D Features for this map. 

   <img src="https://github.com/theaidenlab/juicebox/wiki/images/annotations.png" alt="Annotations">
7. You will see a series of yellow boxes and cyan points loaded. The cyan points denote the exact peaks.

   <img src="https://github.com/theaidenlab/juicebox/wiki/images/domains_peaks.png" alt="Domains and peaks" align=center>
8. These are the contact domains and peaks that we found when analyzing this map. Now let's see what other annotations look like here. Go to the Annotations menu and click Load Basic Annotations again. Click on GM12878 and select the H3K36me3 track and the CTCF track. 

   <img src="https://github.com/theaidenlab/juicebox/wiki/images/basic.png" alt="Annotations menu">

9. You can line up what you see in the heat map with the tracks. Right click on the heat map and select Enable straight edge. Then move around on the map to see the features lined up with the tracks. 

   <img src="https://github.com/theaidenlab/juicebox/wiki/images/straight_edge.png" alt="Straight edge">
10. There are many more functions to explore in Juicebox -- enjoy!  Or try [our tutorial](Visualization) next.

