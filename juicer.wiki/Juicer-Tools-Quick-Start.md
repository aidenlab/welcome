<img src="https://github.com/theaidenlab/juicer/wiki/images/graphic_juicer_tools.png" width="100%" alt="Juicer Tools"/>

This Quick Start guide shows you how to create your own .hic file using [Pre](Pre) and extract the data using [Dump](https://github.com/theaidenlab/juicer/wiki/Data-Extraction).

The Juicer command line tools also include powerful feature annotation and analysis algorithms; please explore the links on the right for more on those. 

1. Download the [Juicer command line tools jar](Download).
2. Download the [test data set](data/test.txt.gz)
3. To launch the command line tools, run the shell script [juicebox](https://github.com/theaidenlab/juicer/blob/master/UGER/scripts/juicebox) on Unix or MacOS or type
    ```
    java -Xms512m -Xmx2048m -jar juicer_tools.jar pre data/test.txt.gz data/test.hic hg19
    ```
4. A .hic file should be produced. In [Juicebox](https://github.com/theaidenlab/juicebox/wiki/), click File -> Open.. and
   then click the Local button at the bottom of the dialog. Navigate to the `data/` directory and click on `test.hic`
5. The file should load. Click on chromosome 1. Use the resolution slider to 
    go to 1Mb resolution (the resolution between 2.5Mb and 500Kb). 
6. To verify everything worked correctly, move your mouse until it hovers over
    the bin at 100mb x 100mb.
7. The hover text on the right should read:

      ```
      1:100,000,001-101,000,000
      1:100,000,001-101,000,000
      observed value = 410
      expected value = 339.504
      O/E = 1.208
      ```

8. To extract the data matrices from the .hic file, go to the command prompt.
9. Type:
      `java -jar juicer_tools.jar dump observed KR data/test.hic 1 1 BP 2500000 chr1.txt`
10. The file chr1.txt contains the observed matrix of chromosome 1 with 
    KR (Balanced) normalization at 2.5Mb resolution.


