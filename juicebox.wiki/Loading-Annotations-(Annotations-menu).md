## `Loading basic annotations`
Make sure you have a Hi-C map open. From the *Annotations* menu, click *Load Basic Annotations...*

<img width=227 height=96 src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/navigation/image002.png" class="centered" alt=""/><br>
A pop up window titled *Available Features* will appear.

<img width=411 height=357 src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/navigation/image004.png" class="centered" alt=""/>

Check the required feature(s) and press "OK". The new annotation will be downloaded to your Juicebox viewer and displayed above and to the left of the main map window. Note that some annotations, like the gene track, are clickable, showing more information.  

In order to remove the annotation, right click on the track, and select "Remove track", or you can also repeat the steps above and uncheck the annotation(s) you want to remove.

Additional annotations include:
<center>    
<br>Gene reference:<br>
<img width=434 height=55 src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/navigation/image006.png" alt=""/>
<br>Coverage annotation:<br>																<img width=434 height=70 src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/navigation/image008.png" alt=""/>											<br>GM12878 CTCF orientation annotation:<br>
<img width=434 height=135 src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/navigation/image010.png" alt=""/>
<br>Eigenvector:<br>
<img width=434 height=87 src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/navigation/image012.png" alt=""/><br>


----

<div align="left">


## `Loading 1D Tracks` 

You can also load you your own bed or wig track files. From the *Annotations* menu, click *Load Basic Annotations...*

<img width=411 height=357 class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/navigation/image014.png" alt=""/>

Click *Add 1D...*. A file explorer window will open.  Select your track file. The new track file name will appear in *Available Features* menu. Click "OK" to show your track. In case of an unsupported file format, the following error will be displayed:

<img width=434 height=125 class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/navigation/image016.png" alt=""/>

----

## `Adding 2D annotations` 

Some of the annotations in Juicebox are marked on the main map. An example is available in the *GM2878 in situ MBOI primary + replicate* map. After opening this map, a "Data-set specific 2D features" annotations are available in the annotations menu. Use the `F2` key to toggle the visibility of 2D annotations.

Juicebox supports the <a href="https://bedtools.readthedocs.io/en/latest/content/general-usage.html#bedpe-format">bedpe</a> format for 2D annotations and uses this format for writing loop and domain files. Bedpe files are tab-delimited. The header line looks like this:

```
#chr1  x1	 x2	    chr2   y1	      y2	  name	score  strand1  strand2	color [optional fields]
chr5   85000000  89000000   chr5   85000000   89000000    .     .      .        .       255,0,0
``` 

Note:

- Make sure your chromosome names are the same as the ones that appear in the Hi-C map.

- Keep the header line.

- The file is tab delimited.

----
## `Custom Annotations`

You can also create custom data-specific 2D annotations to visualize peaks and domains. In order to create a custom annotation, open a Juicebox map (*GM2878 in situ MBOI primary + replicate*, for example) and hold the shift key over a region of the map. A moving cross-hairs will appear as you move the mouse.

<p align="center">
<img width=428 height=300 class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/navigation/crosshairs.png" alt="">
</p>

In order to create a custom 2D annotation for a particular region of interest, hover the mouse over a region of the map that is enriched higher compared to the surrounding area. By clicking on this region, a small box will appear on both sides of the diagonal line indicating the successful annotation.	

<p align="center">
<img width=428 height=300 class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/navigation/pointannotation.png" alt="">
</p>

To create a custom annotation for a broader region, hold the shift key and use the mouse to again create the moving cross hairs. Click and drag the mouse to highlight a square around the area that is to be annotated. A green rectangle will appear and border the region of interest.  If you annotate close to the diagonal, the annotation will auto-capture the region as a square.

<p align="center">
<img width=428 height=300 class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/navigation/rectangle.png" alt="">
<img width=428 height=300 class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/navigation/square.png" alt="">
</p>

----

## `Load ENCODE tracks`

You can also use Juicebox to display ENCODE tracks. From the *Annotations* menu, click *Load Basic Annotations...*

<img width=218 height=93 class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/navigation/image020.png" alt="">

Click *Load ENCODE Tracks*. The *Encode Production Data* screen will appear:

<img width=434 height=387 class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/navigation/image022.png" alt="">

You can use free text to search through any of the track fields, or scroll through the tracks list. Check the required ENCODE track(s) and click "Load" to load the data. A track will be added to top and left of the main map.

<img width=435 height=67 class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/navigation/image024.png" alt=""/>							

----
## `Configure tracks`

With some tracks, you can change basic appearance. Right click on a track and select *Configure track...*.

<img width=209 height=81 class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/navigation/image026.png" alt=""/>	

A new screen will appear, where you can change track Name, Min/Max values Scale, and colors for positive and negative values.

<img width=245 height=222 class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/navigation/image028.png" alt=""/>

----

## `Editing Annotations` 

Annotations can be edited within Juicebox. Users can adjust an annotation's position, delete it, change its color, or add a text attribute to document any interesting features. Hand annotations can be edited directly, following the directions below. Loaded 2D annotations can also be edited by copying them to hand annotations. To do this, load a basic 2D annotation, then go to *Annotations* → *2D Annotations* → *Copy to Hand Annotations*. The loaded annotation can now be edited as a hand annotation.

----    
## `Adjusting Size`

To adjust the size of the annotation, hover over the upper lefthand or lower righthand corner, inside of the annotation.

<p align="center">
<img width=428 height=300 class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/custom/1.png" alt=""></p>

Click and drag the corner to the desired size. Release the mouse to create the change.

<p align="center">
<img width=428 height=300 class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/custom/2.png" alt="">
</p>

----

## `Adding/Changing Attributes`
Attributes can be added to annotations to mark interesting features. For example, an attribute name could be "Feature Quality", and its value could be "Poor,""High," etc. To add an attribute, right click an annotation and go to *Configure Feature* → *Change Attributes*. An attribute can be added by entering a name, or descriptive category, and value. The attribute will be displayed as a part of the hover text on the righthand bar of the main window.
<img width=428 height=300 class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/custom/3.png" alt="">

To edit an attribute, right click an annotation, go to *Configure Feature* → *Change Attributes*. The value of the attribute can now be changed, as shown below.

<img width=428 height=300 class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/custom/4.png" alt="">

----
## `Changing Color`

The color of an annotation can be changed by right clicking an annotation and going to *Configure Feature* → *Change Color*.

----

## `Deleting`

Individual annotations can be deleted by right clicking an annotation and going to *Configure Feature* → *Delete*. The last added annotation can also be removed by going to *Annotations* → *Hand Annotations* → *Undo Annotation*, or by pressing "Z", the shortcut key.

----

## `Exporting Hand Annotations`

A set of hand annotations can be exported by going to *Annotations* → *Hand Annotations* → *Export...* 

Exported annotations can be loaded as a basic 2D annotation, by selecting the file by going to *Annotations* → *Load Basic Annotations...* → *Add 2D...*

Let's see some more features for [exploring the map](Exploring-the-Data).
