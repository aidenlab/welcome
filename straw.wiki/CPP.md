## Compiling Straw in C++

```bash
g++ -std=c++0x -o straw main.cpp straw.cpp -lcurl -lz
```
- You must have cURL installed.
- straw must be compiled with the `-lz` flag to include the zlib.h library: 
- On Linux, you may need to use this flag to compile: `-std=c++11`

On Windows, we've compiled using Cygwin. Order matters, put the linking libraries last:

```bash
g++ -o straw main.cpp straw.cpp -lz -std=c++11
```
----
## Running straw in C++
Usage: 
   
```bash
straw <NONE/VC/VC_SQRT/KR> <hicFile> <chr1>[:x1:x2] <chr2>[:y1:y2] <BP/FRAG> <binsize>
```

Extract all reads on chromosome X at 1MB resolution with no normalization in local file "HIC001.hic" 
   
```bash
straw NONE HIC001.hic X X BP 1000000
```

Extract reads between 1MB and 7.5MB on chromosome 1 at 25KB resolution with KR (balanced) normalization:

```bash
straw KR HIC001.hic 1:1000000:7400000 1:1000000:7400000 BP 25000
```
----
*For questions, please use*
[the Google Group](https://groups.google.com/forum/#!forum/3d-genomics).
