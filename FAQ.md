## Version issues (1.x vs 2.x)

Juicer and Juicer Tools are under active development, and we have not made official releases for version 2 yet. In general, while we try to maintain backward compatibility, it is not always possible. Some general guidelines:
* Files built with Juicer Tools 1.x should be readable by all future 2.x jars for most tools (HiCCUPS, Arrowhead, etc).
* For file writing tools (`pre` and `addnorm`) the same jar must be used (i.e. if `pre` was called from a 1.x jar, `addnorm` must also be called from a `1.x` jar). This is because 2.x jars only write the latest `v9` of the `.hic` file. 
* To upgrade your `v8` `.hic` files to `v9`, you can either rebuild files using the `merged_nodups` or use the [EMT Tool](https://github.com/sa501428/hic-emt) to build a newer `.hic` file from an older one.

## KR is not available for a particular chromosome/region

The KR algorithm sometimes does not converge for a particular region/chromosome. When the normalization fails for a chromosome at a specific resolution, the `.hic` file does not contain the normalization vector for that resolution as well as higher resolutions. More recently, we have added a new normalization method, called SCALE to remedy this. You can use `addNorm` in newer versions of juicer tools to use SCALE instead of KR.

## Normalization failing for fragment (FRAG) resolutions or FRAG resolution questions in general

We've actually moved away from fragment resolution maps. Unless you are doing some very specific/specialized development, you probably don't need them. Going forward, Juicer 2 will no longer build fragment resolutions. Instead, you can build higher basepair (BP) resolution maps. Remove the `-f` flag for `pre` or *add* the `-F` flag for `addnorm` to ignore these FRAG resolutions.

## Juicer pre is taking a very long time

If you are assembling a genome, don't try to build a hic map with thousands of contigs. Checkout the very detailed walkthrough on the [DNAZoo Website](https://www.dnazoo.org/methods).

## How can I access published Hi-C data?
You can use Juicebox and Juicer command line tools directly on URLs. Check out [our data page](http://aidenlab.org/data.html) for those links. We recommend this method as opposed to downloading full .hic files, but if there's an experiment you plan to explore a lot and/or you have a bad internet connection, you can download locally.

If you would like to download a local version of a .hic file, check out the GEO repository for the experiment. We have also put some maps up in a [Box mirror](https://bcm.app.box.com/v/aidenlab)

You can also parse the default properties file at http://hicfiles.tc4ga.com/juicebox.properties to grab the web address of the file you're interested in.

## How do I create my own .hic files from my own data?
Check out the Juicer command line tools [pre command](https://github.com/theaidenlab/juicer/wiki/Pre)

## What's the format of the restriction site file?
See [these directions](https://github.com/theaidenlab/juicer/wiki/Pre#restriction-site-file-format)

## Error: the chromosome combination appears in multiple blocks
Please see [this thread](http://www.aidenlab.org/forum.html?place=msg%2F3d-genomics%2F2w1OGHo5XdM%2FcIiHCuP_AQAJ)

## Juicer (pre) is slow and/or takes a lot of memory
Try running without a fragment map.  For the Juicer pipeline, use the flag `-x` to exclude fragment maps. At the [Pre](https://github.com/theaidenlab/juicer/wiki/Pre) stage, simply don't send in the restriction site file.

If you are only interested in a few resolutions, you can call Pre with the `-r` flag.  E.g., to create a file with only 25Kb and 10Kb binned maps, do `-r 5000,10000`

## I have already binned and/or normalized data, how do I create a .hic file?
Use [Pre](https://github.com/theaidenlab/juicer/wiki/Pre) with the nine column "score" format.  See https://github.com/theaidenlab/juicer/wiki/Pre#short-with-score-format

## My question wasn't answered here
Please search the [3D genomics forum](http://aidenlab.org/forum.html) and ask your question there


