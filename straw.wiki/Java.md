## `Installing Straw in Java`

You'll first need to download the Java Straw jar and add it as a library dependency.

----

## `Using Straw in Java`

Let's create hic dataset object. If you want to cache portions of the file, set the corresponding boolean to True. This uses more RAM, but if you want to repeatedly query nearby regions it can improve the speed of the requests. 

```java
boolean useCache = false;
String filename = "file.hic";
Dataset ds = HiCFileTools extractDatasetForCLT(filename, false, useCache, false);
```

Set the desired normalization. 

```java
NormalizationType norm = NormalizationHandler.VC;
System.out.println("Norm being used: " + norm.getLabel());
```


If you want to check for multiple possible normalizations and pick it based on its availability, use:

```java
NormalizationType norm = NormalizationPicker.getFirstValidNormInThisOrder(ds, new String[]{"KR", "SCALE", "VC", "VC_SQRT", "NONE"});
System.out.println("Norm being used: " + norm.getLabel());
```

Let's now retrieve the chromosomes in an array.
```java
Chromosome[] chromosomes = ds.getChromosomeHandler().getChromosomeArrayWithoutAllByAll();
```

Let's then specify a resolution and iterate through the chromosomes (intra chromosomal for now):
```java

    int resolution = 5000;

    for (Chromosome chromosome : chromosomes) {
        Matrix matrix = ds.getMatrix(chromosome, chromosome);
        if (matrix == null) continue;
        MatrixZoomData zd = matrix.getZoomData(new HiCZoom(resolution));
        if (zd == null) continue;

        // your code here
    }
```
`zd` is now a MatrixZoomData object that contains pointers to the data. Let's show 2 different ways to access data.

Option 1: iterate on all the data for the whole chromosome in sparse format (upper triangular matrix only).
 ```java

            Iterator<ContactRecord> iterator = zd.getNormalizedIterator(norm);
            while (iterator.hasNext()) {
                ContactRecord record = iterator.next();
                // now do whatever you want with the contact record
                int binX = record.getBinX();
                int binY = record.getBinY();
                float counts = record.getCounts();

                // binX and binY are in BIN coordinates, not genome coordinates
                // to switch, we can just multiply by the resolution
                int genomeX = binX * resolution;
                int genomeY = binY * resolution;

                if (counts > 0) { // will skip NaNs

                    // do task

                    // the iterator only iterates above the diagonal
                    // to also fill in data below the diagonal, flip it
                    if (binX != binY) {
                        binX = record.getBinY();
                        binY = record.getBinX();
                        counts = record.getCounts();

                        // do task
                    }
                }
            }
```

Option 2: extract data for a given region within specified boundaries

```java

            // choose your setting for when the diagonal is in the region
            boolean getDataUnderTheDiagonal = true;

            // our bounds will be binXStart, binYStart, binXEnd, binYEnd
            // these are in BIN coordinates, not genome coordinates
            int binXStart = 500, binYStart = 600, binXEnd = 1000, binYEnd = 1200;
            List<Block> blocks = zd.getNormalizedBlocksOverlapping(binXStart, binYStart, binXEnd, binYEnd, norm, getDataUnderTheDiagonal);
            for (Block b : blocks) {
                if (b != null) {
                    for (ContactRecord rec : b.getContactRecords()) {
                        if (rec.getCounts() > 0) { // will skip NaNs
                            // can choose to use the BIN coordinates
                            int binX = rec.getBinX();
                            int binY = rec.getBinY();

                            // you could choose to use relative coordinates for the box given
                            int relativeX = rec.getBinX() - binXStart;
                            int relativeY = rec.getBinY() - binYStart;

                            float counts = rec.getCounts();
                        }
                    }
                }
            }
        


        // to iterate over the whole genome
        for (int i = 0; i < chromosomes.length; i++) {
            for (int j = i; i < chromosomes.length; i++) {
                Matrix matrix = ds.getMatrix(chromosomes[i], chromosomes[j]);
                if (matrix == null) continue;
                MatrixZoomData zd = matrix.getZoomData(new HiCZoom(resolution));
                if (zd == null) continue;

                if (i == j) {
                    // intra-chromosomal region
                } else {
                    // inter-chromosomal region
                }
            }
        }
    
    ```
