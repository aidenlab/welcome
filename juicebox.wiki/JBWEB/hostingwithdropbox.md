# Hosting with Dropbox/Drive/GEO

While you can certainly use Amazon S3, Azure, and other file hosting services to store your .hic files, Dropbox works just as well and is quite easy to set up! 
We'll go through a quick tutorial so you can see how easy it is to share results with your collaborators.
We've uploaded sample files to [https://www.dropbox.com/sh/inf1f96r5io5io6/AAAa95E6NXSWKHKxLp2dy4p8a?dl=0](https://www.dropbox.com/sh/inf1f96r5io5io6/AAAa95E6NXSWKHKxLp2dy4p8a?dl=0)
The first step is to upload your file to dropbox, and then copy a link to the .hic file.


<left>
<img width="70%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/dropbox1.png" alt="pic of search/multi search"/></left>	

<left>
<img width="70%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/dropbox2.png" alt="pic of search/multi search"/></left>	

For this particular example, the following file link was created: [https://www.dropbox.com/s/u2m6dm7putuwr58/imr90_intra_nofrag_30.hic?dl=0](https://www.dropbox.com/s/u2m6dm7putuwr58/imr90_intra_nofrag_30.hic?dl=0)

> Juicebox Desktop can also load Dropbox URLs! Simply go to File. 
File → Open... → URL... and paste the link from above.

1. Go to [https://aidenlab.org/juicebox/](https://aidenlab.org/juicebox/)
2. Select `Load Map → URL`
3. Paste the URL copied above into the text box and hit enter

> Note: choosing "Dropbox File" will load your Dropbox folder; choosing "Google Drive File" will load your Google Drive.

<left>
<img width="35%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/dropbox4.png" alt="pic of search/multi search"/></left>	

<left>
<img width="70%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/dropbox5.png" alt="pic of search/multi search"/></left>	

The map will then load. You can do everything you would do with a .hic file. You can also upload your 1D and 2D annotation files to Dropbox and load them into the visualization using Load Tracks → Track URL. Share links can then be generated; here's a fully Dropbox hosted link: [https://tinyurl.com/y8996w5r](https://tinyurl.com/y8996w5r)

> Juicebox Web allows the use of local .hic and annotation files; however, share links generated with such files cannot be sent to collaborators. This is because your local file system isn't accessible to other users. Files must be uploaded to Dropbox, Amazon S3, Box, Azure, Google Drive, GEO, etc. and a URL generated in order to be shared.

<left>
<img width="70%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/dropbox6.png" alt="pic of search/multi search"/></left>	

----

# Loading files from GEO

If you're interested in published data from a paper that performed Hi-C experiments, you can see if they've uploaded their processed data to GEO. For example, let's look at this series: [https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE104333](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE104333)
Scroll down and right-click the ftp link next to the file 180min_withdraw_combined.hic

> You must copy the **ftp** link, not the http link.

<left>
<img width="70%" class="centered" src="https://raw.githubusercontent.com/aidenlab/welcome-images/main/juicebox.images/JBWEB_images/dropbox7.png" alt="pic of search/multi search"/></left>	

Now go to a fresh instance of [Juicebox](https://igv.org/web/jb/test/juicebox.html) and click `Load Map → URL`. Paste the link address  you just copied. As with Dropbox files and any other URL, you can use Juicebox as you normally would.









