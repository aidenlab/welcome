## Loading 1D Annotations

Let's load some ChIP-Seq tracks from ENCODE.
1. Click the `Load Tracks` button on the top panel
2. Click `ENCODE`.

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingannotations_1.png" alt="pic of search/multi search"/></left>

The first time the tracks are loaded, it may take 10-15 seconds.

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingannotations_2.png" alt="pic of search/multi search"/></left>

All the ENCODE tracks available for this genome appear. We are going to filter in order to find the tracks we want to load. 

1. Type `GM12878 CTCF Bernstein` 
2. Select the combined signal p-value track. 
3. Click `Go`.

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingannotations_3.png" alt="pic of search/multi search"/></left>

1. Now click `Load Tracks → ENCODE again`
2. Search for `GM12878 H3K36me3 Bernstein`
3. Select the signal p-value track. 
4. Click `Go`. 

<left>
<img width="75%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingannotations_4.png" alt="pic of search/multi search"/></left>

We can edit how these 1D annotations appear in the visualization using the Gear icon next to the track.

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingannotations_5.png" alt="pic of search/multi search"/></left>


1. Use `Set track name` to relabel the annotations to `CTCF` and `H3K36me3` respectively.
2. Use `Set track color` to change the colors for both 1D tracks.

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingannotations_6.png" alt="pic of search/multi search"/></left>

----
## Loading 2D Annotations
Select `Load Tracks` in the top menu bar and click `ENCODE`. 

Search for `GM12878 domains`. Select the one with all the replicates. 

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loading2d_1.png" alt="pic of search/multi search"/></left>

Repeat the steps above and search for  `GM12878 long range` for this map. Select the one with all the replicates.

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loading2d_2.png" alt="pic of search/multi search"/></left>

Here is a link to the current state: [https://tinyurl.com/ybcawels](https://tinyurl.com/ybcawels)

You will see a series of yellow boxes and cyan points loaded. The yellow boxes denote contact domains. The cyan points denote chromatin loops, and as such, are small. These are the contact domains and loops that we found when analyzing this map. These calls were made with the automated [Juicer pipeline](https://github.com/aidenlab/Juicer/wiki)

<left>
<img width="70%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loading2d_3.png" alt="pic of search/multi search"/></left>

You can edit the 2D annotations by selecting the 3 bars icon and then clicking 2D Annotations. This panel allows you to selectively hide 2D annotations (eye icon), change the color of annotations (color box), change the drawing order of overlapping annotations (up/down arrows), or remove an annotation (trash icon).

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loading2d_4.png" alt="pic of search/multi search"/></left>

----

## Putting together 1D and 2D annotations.
You can line up what you see in the heat map with the tracks. Hold the Shift key to enable the straight edge as you click and drag the mouse to pan around the map.

<left>
<img width="70%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/1dand2d.png" alt="pic of search/multi search"/></left>















