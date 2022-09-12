## Loading 1D Annotations
Let's load some ChIP-Seq tracks from ENCODE. 

1. Click the `Show Annotation Panel` button on the lower right side of your screen.
2. Click the `1D Annotation` tab at the top.
3. Click `Load ENCODE Tracks.`

All the ENCODE tracks available for this genome appear. We are going to filter in order to find the tracks we want to load. 

1. Type `GM12878 CTCF Bernstein`
2. Mark the check box next to the signal p-value track. 
3. Click `Load`.

<left>
<img width="70%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBDesktop/loadingannotations.png" alt="pic of search/multi search"/></left>

1. Now click `Load ENCODE Tracks` again
2. Clear the filter
3. Type `GM12878 H3K36me3 Bernstein`
4. Mark the check box next the signal track. 
5. Click `Load`.

 We can edit how these annotations appear in the visualization using the Annotation Panel.

1. Relabel `ENCFF906RJB.bigWig` to `H3K36me3` and `ENCFF797LSC.bigWig` to `CTCF`.
2. Change the color for the `H3K36me3` track to green by clicking the colored box next to the track. 
----
## Loading 2D annotations

Click `View` in the menu bar and go to `Show Annotation Panel`. Click the top tab for `2D Annotations` and then type `GM12878` into the filter box.

<left>
<img width="70%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBDesktop/loadingannotations2.png" alt="pic of search/multi search"/></left>

Select `GM12878 in situ Hi-C` under both the `Loops` and `Domains` for this map.

<left>
<img width="70%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBDesktop/loadingannotations3.png" alt="pic of search/multi search"/></left>

Exit out of the `Annotation Panel`. You will see a series of yellow boxes and cyan points loaded. The yellow boxes denote contact domains. The cyan points denote chromatin loops, and as such, are small. These are the contact domains and loops that we found when analyzing this map. These calls were made with the automated [Juicer pipeline](https://github.com/aidenlab/Juicer/wiki) and are also available via ENCODE.

<left>
<img width="70%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBDesktop/loadingannotations4.png" alt="pic of search/multi search"/></left>

### `bedpe` file format 
The [`bedpe`](https://bedtools.readthedocs.io/en/latest/content/general-usage.html#bedpe-format) format is used for annotating 2D features, such as chromatin loop and contact domains. Bedpe files are tab-delimited. The header line looks like this:

```
#chr1  x1	 x2	    chr2   y1	      y2	  name	score  strand1  strand2	color [optional fields]
chr5   85000000  89000000   chr5   85000000   89000000    .     .      .        .       255,0,0
``` 

Many of our software tools use `bedpe` files as direct inputs or outputs.

----
## Putting together 1D and 2D Annotations

You can line up what you see in the heat map with the tracks.  
1. Right click on the heat map
2. Select `Enable straight edge`. 
3. Move around on the map to see the features lined up with the tracks. 
> Press F2 to turn on and off the 2D annotations.

<left>
<img width="60%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBDesktop/loadingannotations5.png" alt="pic of search/multi search"/></left>

You’ll notice that the CTCF peaks seem to line up with the focal cyan loops in the map, and that the H3K36me3 track seems to line up with domain boundaries. These are two key findings from the Rao and Huntley, et al. Cell 2014 paper. This discovery was made using Juicebox by qualitatively visualizing the data in just the same way. Further technical analyses then showed that CTCF does appear to mediate loop formation and domains are decorated by differing epigenetic markers. See the Sanborn and Rao, et al. PNAS 2015 paper for more details!

Now let’s look at a different region and see what else we can discover. 

1. Turn off the straight edge (right click on the map to bring up the popup)
2. Remove the H3K36me3 track by right clicking it and then clicking `Remove`.
3. Turn off the 2D annotations by clicking `F2`. 
4. In the `Chromosomes` menu bar, choose `X` for both the left and right chromosomes.
5. Click on the refresh button. Both the left and top chromosomes are now displaying are now using chromosome X.
6. Use the `Resolution` menu slider and choose 25 KB.
7. Navigate to `chrX:114000000-134000000`. 
8. Click on Color range (the label above the slider) and type 168 for the maximum value. (You can also adjust the maximum of the color range slider by clicking the + or – button.) 
9. Slide the right slider to around 160. 

<center>
<img width="40%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBDesktop/loadingannotations6.png" alt="pic of search/multi search"/></center>

You will see a superloop on chromosome X, around the intersection between 115MB and 131MB.

<left>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBDesktop/loadingannotations7.png" alt="pic of search/multi search"/></left>

There also appears to be a series of CTCF peaks. This superloop was another discovery and led to further research into this phenomenon on the X inactive chromosome (see Darrow and Huntley et al. PNAS 2016) 





















