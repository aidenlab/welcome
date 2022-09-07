# Comparing Maps (Desktop)
----
## Load a second map

Continuing with the previously loaded GM12878 map, let’s load another Hi-C map and see if we can discover differences between cell lines!

1. Go to chromosome 21 
2. Click twice to zoom in 
3. Draw a box while holding down the `Alt` key so that you’re looking at 28,000 KB to 30,000 KB. Make sure the resolution is 5KB.
4. Click `File → Open Control`.
5. Load the `ENCODE IMR90 MboI MAPQ 30` map.
6. Go to `Show` on the toolbar and select `Control`
7. Change the `Normalization` on the right to be `Balanced`.

> You can press F1 to toggle between Observed and Control.

As you can see, the regions look quite different!

----
## VS Mode
Another way to examine the data is the VS mode view.
1. Go to `Show` on the toolbar
2. Select `Observed vs Control`

Observed (first loaded map - GM12878) is below the diagonal; control (second loaded map - IMR90) is above the diagonal.

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBDesktop/comparingmapsdesktop.png" alt="pic of search/multi search"/></left>

> You can see in the `Show` list that there are several different ways to compare two maps visually.

Let's explore these differences by bringing in additional ENCODE data.
1. Click the `Show Annotation Panel` in the lower right corner
2. Click the `1D Annotations` tab
3. Click `Load Basic Annotations...`
4. Load the `Genes` track
5. Back in the 1D Annotations tab, click `Load ENCODE...`
6. Load `RNA-seq`, `H3K4me3`, and `CTCF` tracks for both `GM12878` and `IMR-90`

You’ll notice that there is a peak in the RNA-seq track for IMR-90 on the gene ADAMTS1, and that there’s a peak in the IMR-90 H3K4me3 track; neither of these are present on the respective GM12878 tracks. H3K4me3 is an activation mark. ADAMTS1 encodes a protein involved in fibroblast migration and is inactive in GM12878 but active in IMR90.

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBDesktop/comparingmapsdesktop2.png" alt="pic of search/multi search"/></left>















