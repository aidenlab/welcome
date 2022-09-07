## Load another Map
Continuing with the previously loaded GM12878 map, let’s load another Hi-C map and see if we can discover differences between cell lines!

1. Go to chromosome 21 (click on the 3 bars icon and change chromosome).
2. Click twice to zoom in 
3. Draw a box while holding down the Alt key (Option key on Macs) so that you’re looking at 28,000 KB to 30,000 KB. 

Alternatively, just type in `ADAMTS1` in the location text box to jump to the gene location directly. Or type in `21:27,810,323-30,270,322 21:27,784,825-30,244,824` into the location text box and hit enter. Now let's load the IMR-90 Map.

Click the add map pane `+` icon in the top right. 

<center>
<img width="40%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/comparingmaps.png" alt="pic of search/multi search"/></center>

This creates an empty new map panel next to the previous map.

<left>
<img width="70%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/comparingmaps_2.png" alt="pic of search/multi search"/></left>

Select `Load Map → ENCODE`, and then search for `IMR-90 1_2`. Select the combined replicate map, ENCFF999YXX. 

<center>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/comparingmaps_3.png" alt="pic of search/multi search"/></center>

>When working with multiple maps, you know which map window you’re operating on because there’s a dark line around it. 

Change the `Norm` for the newly loaded map to be `Balanced`. The map will automatically zoom in to the same region as the first map. As you can see, the regions look quite different!

<center>
<img width="70%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/comparingmaps_4.png" alt="pic of search/multi search"/></center>

Adjust the color scale for the two maps by pressing the +/- buttons next to the red square, or changing the number in the text panel next to it. Change the numbers to be 25 and 15 for the two maps (this reflects that the maps are sequenced to different depths).

<center>
<img width="70%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/comparingmaps_5.png" alt="pic of search/multi search"/></center>

Let's add annotations for the newly loaded IMR90 map. Do so while the IMR90 map is selected with the darker box outline.

1. Select `Load Tracks → ENCODE` to load the 1D annotations. Search for `ENCFF583IZF (CTCF)` and `ENCFF187AAC (H3K36me3)`. Change the colors and names of the tracks using the gear icon.
2. Select `Load Tracks → ENCODE` and search for `IMR-90 domains` and `IMR-90 long range` to load the combined loops and domains for IMR90.
3. Select `Load Tracks → Genome Annotations` and select `Genes` to load the gene track for this assembly. Then highlight the first window (with GM12878) and load genes there as well.

You should see something like this: [https://tinyurl.com/yc6gvqy4](https://tinyurl.com/yc6gvqy4)
<center>
<img width="70%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/comparingmaps_6.png" alt="pic of search/multi search"/></center>

Let's explore these differences by bringing in additional ENCODE data. Load `RNA-seq signal` and `H3K4me3` for both `GM12878` (ENCFF001SCA, ENCFF351WPV) and `IMR-90` (ENCFF000HAN, ENCFF254FBR).

You’ll notice that there is a peak in the RNA-seq track for IMR-90 on the gene ADAMTS1, and that there’s a peak in the IMR-90 H3K4me3 track; neither of these are present on the respective GM12878 tracks. H3K4me3 is an activation mark. ADAMTS1 encodes a protein involved in fibroblast migration and is inactive in GM12878 but active in IMR90. [https://tinyurl.com/y9pwkmrp](https://tinyurl.com/y9pwkmrp)

<center>
<img width="70%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/comparingmaps_7.png" alt="pic of search/multi search"/></center>

----

## Loading as a Control Map

Similar to Juicebox Desktop, you can load a second map into the same panel as the first map. This allows you divide the maps by each other or make a gif-style switch to cycle between the do.
Instead of of adding a second map by using the + button, select the original map and use Load "B" Map. Once the map is loaded, additional buttons should appear.

<center>
<img width="70%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/comparingmaps_8.png" alt="pic of search/multi search"/></center>

- The dropdown can toggle between different views - the A map, B map, A/B, and B/A
- The two arrows allows for switching between the A and B maps
- The circle allows for toggling of a cycle mode, which will automatically switch back and forth between the maps

>Share links generated in this cycling mode (e.g. [https://tinyurl.com/ybabbdtb](https://tinyurl.com/ybabbdtb)) will preserve the switching back and forth between the maps!









