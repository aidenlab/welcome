
## Java Straw Guide

first install the package `javastraw`


If you want to cache portions of the file, set to True. This uses more ram, but if you want to repeatedly query nearby regions it can improve speed. 

First we import `numpy` and `hicstraw`.
```java
boolean useCache = false;
String filename = "file.hic";
```

Create hic dataset object.
```java
Dataset ds = HiCFileTools extractDatasetForCLT(filename, false, useCache, false);
```

Pick desired normalization. This line will check multiple possible norms and pick based on availability.

```java
NormalizationType norm = NormalizationPicker.getFirstValidNormInThisOrder(ds, new String[]{"KR", "SCALE", "VC", "VC_SQRT", "NONE"});
System.out.println("Norm being used: " + norm.getLabel());
```

Set resolution

```java
int resolution = 5000;
```

Grabbing chromosomes.
```java
Chromosome[] chromosomes = ds.getChromosomeHandler().getChromosomeArrayWithoutAllByAll();
```
Iterating through chromosomes (intra chromosomal for now):
```java
for (Chromosome chromosome : chromosomes) {
        Matrix matrix = ds.getMatrix(chromosome, chromosome);
        if (matrix == null) continue;
        MatrixZoomData zd = matrix.getZoomData(new HiCZoom(resolution));
        if (zd == null) continue;
```
Zd is now a data structure that contains pointers to the data. Let's show 2 different ways to access data.

Option 1:
 iterate on all the data for the whole chromosome in sparse format.
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
Option 2:
```java
           // OPTION 2
            // just grab sparse data for a specific region

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
        }
```

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
    }

For Full guide:

https://github.com/sa501428/java-straw/blob/master/src/javastraw/AnnotatedExample.java