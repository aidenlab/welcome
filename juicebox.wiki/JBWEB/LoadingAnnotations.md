## Loading 1D Annotations

Let's load some ChIP-Seq tracks from ENCODE.
1. Click the `Load Tracks` button on the top panel
2. Click `ENCODE Signals`.
3. Search for `GM12878 H3K36me3 Bernstein` in top right corner. 
3. Select the signal p-value track. 
4. Click `Go`. 

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations1.png" alt="pic of search/multi search"/></left>

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations2.png" alt="pic of search/multi search"/></left>

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations3.png" alt="pic of search/multi search"/></left>


<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations4.png" alt="pic of search/multi search"/></left>

The annotation is now loaded and should look like this.

<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations5.png" alt="pic of search/multi search"/></left>


Lets load another annotation! Once again click load tracks and the ENCODE signals, but this time type `GM12878 H3k36me3 Bernstein`.

1. Click the `Load Tracks` button on the top panel
2. Click `ENCODE Signals`.
3. Search for `GM12878 H3k36me3 Bernstein`
4. Click `Go`. 

<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations6.png" alt="pic of search/multi search"/></left>


<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations7.png" alt="pic of search/multi search"/></left>

We can edit how these 1D annotations appear in the visualization using the Gear icon next to the track.

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations72.png" alt="pic of search/multi search"/></left>


1. Use `Set track name` to relabel the annotations to `CTCF` and `H3K36me3` respectively.
2. Use `Set track color` to change the colors for both 1D tracks.

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations8.png" alt="pic of search/multi search"/></left>


<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations9.png" alt="pic of search/multi search"/></left>

----
## Loading 2D Annotations
Select `Load Tracks` in the top menu bar and click `ENCODE`. 

Search for `GM12878 domains`. Select the one with all the replicates. 

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations10.png" alt="pic of search/multi search"/></left>


<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations11.png" alt="pic of search/multi search"/></left>


<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations12.png" alt="pic of search/multi search"/></left>

Repeat the steps above and search for  `GM12878 long range` for this map. Select the one with all the replicates.

Here is a link to the current state: [https://tinyurl.com/ybcawels](https://tinyurl.com/ybcawels)

You will see a series of yellow boxes and cyan points loaded. The yellow boxes denote contact domains. The cyan points denote chromatin loops, and as such, are small. These are the contact domains and loops that we found when analyzing this map. These calls were made with the automated [Juicer pipeline](https://github.com/aidenlab/Juicer/wiki)

You can edit the 2D annotations by selecting the 3 bars icon and then clicking 2D Annotations. This panel allows you to selectively hide 2D annotations (eye icon), change the color of annotations (color box), change the drawing order of overlapping annotations (up/down arrows), or remove an annotation (trash icon).

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations13.png" alt="pic of search/multi search"/></left>

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations14.png" alt="pic of search/multi search"/></left>

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations15.png" alt="pic of search/multi search"/></left>

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations16.png" alt="pic of search/multi search"/></left>

### `bedpe` file format 
The [`bedpe`](https://bedtools.readthedocs.io/en/latest/content/general-usage.html#bedpe-format) format is used for annotating 2D features, such as chromatin loop and contact domains. Bedpe files are tab-delimited. The header line looks like this:

```
#chr1  x1	 x2	    chr2   y1	      y2	  name	score  strand1  strand2	color [optional fields]
chr5   85000000  89000000   chr5   85000000   89000000    .     .      .        .       255,0,0
``` 

Many of our software tools use `bedpe` files as direct inputs or outputs.

----

## Putting together 1D and 2D annotations.
You can line up what you see in the heat map with the tracks. Hold the Shift key to enable the straight edge as you click and drag the mouse to pan around the map.

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/annotations17.png" alt="pic of search/multi search"/></left>















