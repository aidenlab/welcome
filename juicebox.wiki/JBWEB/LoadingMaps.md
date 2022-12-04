## Juicebox Web

We'll start with the lightweight version of Juicebox available on the web. Open a browser and type [`https://aidenlab.org/juicebox`](https://aidenlab.org/juicebox/) or click the hyperlink. 

Juicebox on the Web is run via client side JavaScript. Any hic file can be loaded from a URL – and in particular, .hic files uploaded to Dropbox, GEO, Google Drive, Amazon S3, or any web server can be streamed!

> You can even browse 3D genomics Hi-C maps on your mobile phone. 

Juicebox on the Web makes it easy to browse maps side-by-side and to share exactly what you’re looking at with collaborators. The core functionality of browsing contact maps together with epigenetic marks is the same as Juicebox Desktop.

----

## Loading Maps

<center>
<img width="50%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingmaps_1.png" alt="pic of search/multi search"/></center>

1. Click `Load Map -> ENCODE`
2. Lets try using the "search" function, type `GM12878` and pick the GRch38 Assembly with the most replicates as shown. 

<center>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingmaps_22.png" alt="pic of search/multi search"/></center>

<center>
<img width="75%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingmaps_3.png" alt="pic of search/multi search"/></center>

The genome wide view will load for the .hic file. 

<center>
<img width="75%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingmaps_4.png" alt="pic of search/multi search"/></center>

----

## Zooming in

Let's zoom in on chromosome 17. To select the chromosome from the genome-wide view, you can:
- Click on the three bar "hamburger" icon in the right top corner, then select the chromosome under the dropdown menu
- Click on the region of the Hi-C map corresponding to chromosome 17
- Click on the numbered chromosome axis label

<center>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/hamburger.png" alt="pic of search/multi search"/></center>

This will load the chromosome-wide view.

<center>
<img width="75%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingmaps_5.png" alt="pic of search/multi search"/></center>

<center>
<img width="75%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingmaps_7.png" alt="pic of search/multi search"/></center>

Be sure to click the circular arrows to refresh (circled in red) to apply changes.

<center>
<img width="75%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingmaps_82.png" alt="pic of search/multi search"/></center>

<center>
<img width="75%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingmaps_9.png" alt="pic of search/multi search"/></center>

Let's change the `Norm` (Normalization) to `Balanced`. This balances the map to account for types of experimental bias in the data.

<center>
<img width="75%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingmaps_92.png" alt="pic of search/multi search"/></center>

<center>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingmaps_10.png" alt="pic of search/multi search"/></center>


<center>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingmaps_11.png" alt="pic of search/multi search"/></center>

There are several ways to zoom in a Hi-C map. Let's zoom into the region around 69.4 MB to 72.3 MB. You can use one of the following methods:

- Slide the resolution dropdown to 5 KB. Use your mouse to pan until your position is roughly 69.4 MB to 72.3 MB.


<center>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingmaps_112.png" alt="pic of search/multi search"/></center>


<center>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingmaps_12.png" alt="pic of search/multi search"/></center>

And pan to the region of interest.


- Type in `17:69,357,606-72,237,605 17:69,352,606-72,232,605` in the location text panel and press the enter key. Go to 5 KB if necessary. 


<center>
<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingmaps_113.png" alt="pic of search/multi search"/></center>


- Hold down the Alt key (Option key on Macs) and draw a box that encompasses 69.4 MB to 72.3 MB. Repeat as necessary and use the mouse to pan until you find the right location.

<center>
<img width="75%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/altdrag.png" alt="pic of search/multi search"/></center>

- Zoom in further by clicking; the heat map will be centered at the point you click.
- Use pinch zoom on a mobile device and pan as needed until you're at the target location.
- Type in your gene of interest in the location text box to jump to the location.

You should see the following region:


https://tinyurl.com/2pkpjops

<center>

<img width="100%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/loadingmaps_13.png" alt="pic of search/multi search"/></center>


