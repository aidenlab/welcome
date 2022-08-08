# Install
The easiest way to install is via pip:

```
 python3 -m pip install hic-straw
```

Straw uses the [requests library](http://docs.python-requests.org/en/master/user/install/#install) for support of URLs.  Be sure it is installed.

After importing, you can always see usage via `help(straw)`

```
import straw
help(straw)
```

# Examples

See an example with Google Colab here: [notebook](https://aidenlab.gitbook.io/juicebox/accessing-raw-data)

* Extract all reads on chromosome X at 1MB resolution with no normalization in local file "HIC001.hic" 
   ```python
   import straw
   result = straw.straw('NONE', 'HIC001.hic', 'X', 'X', 'BP', 1000000)
   # the values returned are in x / y / counts
   for i in range(len(result[0])):
      print("{0}\t{1}\t{2}".format(result[0][i], result[1][i], result[2][i]))
   ```
* Extract reads from a URL: chromosome 14 with KR normalization at 2.5Mb resolution, from the Cell 2014 GM12878 combined replicate map:
   ```python
   import straw
   result = straw.straw("KR", "https://hicfiles.s3.amazonaws.com/hiseq/gm12878/in-situ/combined.hic", "14", "14", "BP", 2500000)
   ```
   All the maps listed in the Juicebox menu available at http://hicfiles.tc4ga.com/juicebox.properties

* Extract reads between 1MB and 7.5MB on chromosome 1 at 25KB resolution with KR (balanced) normalization and write to a file:
   ```python
   import straw
   straw.printme("KR", "HIC001.hic", "1:1000000:7500000", "1:1000000:7500000", "BP", 25000, 'out.txt')
   ```
   To get in an array:
   ```python
   import straw
   result = straw.straw("KR", "HIC001.hic", "1:1000000:7500000", "1:1000000:7500000", "BP", 25000)
   ```


* Extract all interchromosomal reads between chromosome 5 and chromosome 12 at 500 fragment resolution with VC (vanilla coverage) normalization:
   ```python
   import straw

   result = straw.straw("VC", "HIC001.hic", "5", "12", "FRAG", 500)
   # the values returned are in results
   for i in range(len(result[0])):
      print("{0}\t{1}\t{2}".format(result[0][i], result[1][i], result[2][i]))
   ```

See the script [straw.py](https://github.com/theaidenlab/straw/blob/master/python/straw.py) for an example of how to print the results to a file.  

# Read header
See the file [read_hic_header.py](https://github.com/theaidenlab/straw/blob/master/python/read_hic_header.py) for a Python script that reads the header of a hic file and outputs the information (including resolutions).
