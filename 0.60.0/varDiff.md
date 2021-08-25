




[matrixStats]: Benchmark report

---------------------------------------



# varDiff() benchmarks

This report benchmark the performance of varDiff() against alternative methods.

## Alternative methods

* N/A


## Data type "integer"
### Data
```r
> rvector <- function(n, mode = c("logical", "double", "integer"), range = c(-100, +100), na_prob = 0) {
+     mode <- match.arg(mode)
+     if (mode == "logical") {
+         x <- sample(c(FALSE, TRUE), size = n, replace = TRUE)
+     }     else {
+         x <- runif(n, min = range[1], max = range[2])
+     }
+     storage.mode(x) <- mode
+     if (na_prob > 0) 
+         x[sample(n, size = na_prob * n)] <- NA
+     x
+ }
> rvectors <- function(scale = 10, seed = 1, ...) {
+     set.seed(seed)
+     data <- list()
+     data[[1]] <- rvector(n = scale * 100, ...)
+     data[[2]] <- rvector(n = scale * 1000, ...)
+     data[[3]] <- rvector(n = scale * 10000, ...)
+     data[[4]] <- rvector(n = scale * 1e+05, ...)
+     data[[5]] <- rvector(n = scale * 1e+06, ...)
+     names(data) <- sprintf("n = %d", sapply(data, FUN = length))
+     data
+ }
> data <- rvectors(mode = mode)
> data <- data[1:4]
```

### Results

### n = 1000 vector

#### All elements
```r
> x <- data[["n = 1000"]]
> stats <- microbenchmark(varDiff = varDiff(x), var = var(x), diff = diff(x), unit = "ms")
```

_Table: Benchmarking of varDiff(), var() and diff() on integer+n = 1000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr    |      min|        lq|      mean|   median|        uq|      max|
|:--|:-------|--------:|---------:|---------:|--------:|---------:|--------:|
|2  |var     | 0.016467| 0.0172115| 0.0184336| 0.017619| 0.0183320| 0.056639|
|3  |diff    | 0.018938| 0.0199750| 0.0211013| 0.020617| 0.0214065| 0.047552|
|1  |varDiff | 0.023174| 0.0245665| 0.0258000| 0.025152| 0.0260825| 0.051969|


|   |expr    |      min|       lq|     mean|   median|       uq|       max|
|:--|:-------|--------:|--------:|--------:|--------:|--------:|---------:|
|2  |var     | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.0000000|
|3  |diff    | 1.150058| 1.160561| 1.144718| 1.170157| 1.167712| 0.8395628|
|1  |varDiff | 1.407299| 1.427331| 1.399615| 1.427550| 1.422785| 0.9175480|

_Figure: Benchmarking of varDiff(), var() and diff() on integer+n = 1000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/varDiff,integer,n=1000,benchmark.png)

### n = 10000 vector

#### All elements
```r
> x <- data[["n = 10000"]]
> stats <- microbenchmark(varDiff = varDiff(x), var = var(x), diff = diff(x), unit = "ms")
```

_Table: Benchmarking of varDiff(), var() and diff() on integer+n = 10000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr    |      min|        lq|      mean|    median|        uq|      max|
|:--|:-------|--------:|---------:|---------:|---------:|---------:|--------:|
|2  |var     | 0.057814| 0.0620055| 0.0674182| 0.0654900| 0.0718715| 0.092694|
|1  |varDiff | 0.078497| 0.0833665| 0.0918432| 0.0878905| 0.0985555| 0.168082|
|3  |diff    | 0.130929| 0.1441680| 0.1534088| 0.1509175| 0.1611595| 0.199075|


|   |expr    |      min|       lq|     mean|   median|       uq|      max|
|:--|:-------|--------:|--------:|--------:|--------:|--------:|--------:|
|2  |var     | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|1  |varDiff | 1.357751| 1.344502| 1.362292| 1.342045| 1.371274| 1.813300|
|3  |diff    | 2.264659| 2.325084| 2.275481| 2.304436| 2.242328| 2.147658|

_Figure: Benchmarking of varDiff(), var() and diff() on integer+n = 10000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/varDiff,integer,n=10000,benchmark.png)

### n = 100000 vector

#### All elements
```r
> x <- data[["n = 100000"]]
> stats <- microbenchmark(varDiff = varDiff(x), var = var(x), diff = diff(x), unit = "ms")
```

_Table: Benchmarking of varDiff(), var() and diff() on integer+n = 100000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr    |      min|        lq|      mean|   median|       uq|      max|
|:--|:-------|--------:|---------:|---------:|--------:|--------:|--------:|
|2  |var     | 0.431049| 0.4551065| 0.5140164| 0.476812| 0.537810| 0.772107|
|1  |varDiff | 0.560788| 0.5827865| 0.6986960| 0.598159| 0.636758| 7.013415|
|3  |diff    | 1.036736| 1.0770515| 1.3542897| 1.145137| 1.358397| 6.742992|


|   |expr    |      min|       lq|     mean|   median|       uq|      max|
|:--|:-------|--------:|--------:|--------:|--------:|--------:|--------:|
|2  |var     | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|1  |varDiff | 1.300984| 1.280550| 1.359287| 1.254496| 1.183983| 9.083476|
|3  |diff    | 2.405146| 2.366592| 2.634721| 2.401653| 2.525793| 8.733235|

_Figure: Benchmarking of varDiff(), var() and diff() on integer+n = 100000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/varDiff,integer,n=100000,benchmark.png)

### n = 1000000 vector

#### All elements
```r
> x <- data[["n = 1000000"]]
> stats <- microbenchmark(varDiff = varDiff(x), var = var(x), diff = diff(x), unit = "ms")
```

_Table: Benchmarking of varDiff(), var() and diff() on integer+n = 1000000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr    |       min|        lq|      mean|    median|        uq|      max|
|:--|:-------|---------:|---------:|---------:|---------:|---------:|--------:|
|2  |var     |  4.670799|  4.841009|  5.368097|  5.062539|  5.350697| 11.49339|
|1  |varDiff |  6.065771|  6.334729|  7.247055|  6.770384|  7.205823| 13.16935|
|3  |diff    | 10.958685| 11.284448| 13.620769| 11.950078| 13.879137| 28.33761|


|   |expr    |      min|       lq|     mean|   median|       uq|      max|
|:--|:-------|--------:|--------:|--------:|--------:|--------:|--------:|
|2  |var     | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|1  |varDiff | 1.298658| 1.308556| 1.350023| 1.337349| 1.346707| 1.145820|
|3  |diff    | 2.346212| 2.331012| 2.537355| 2.360491| 2.593893| 2.465558|

_Figure: Benchmarking of varDiff(), var() and diff() on integer+n = 1000000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/varDiff,integer,n=1000000,benchmark.png)



## Data type "double"
### Data
```r
> rvector <- function(n, mode = c("logical", "double", "integer"), range = c(-100, +100), na_prob = 0) {
+     mode <- match.arg(mode)
+     if (mode == "logical") {
+         x <- sample(c(FALSE, TRUE), size = n, replace = TRUE)
+     }     else {
+         x <- runif(n, min = range[1], max = range[2])
+     }
+     storage.mode(x) <- mode
+     if (na_prob > 0) 
+         x[sample(n, size = na_prob * n)] <- NA
+     x
+ }
> rvectors <- function(scale = 10, seed = 1, ...) {
+     set.seed(seed)
+     data <- list()
+     data[[1]] <- rvector(n = scale * 100, ...)
+     data[[2]] <- rvector(n = scale * 1000, ...)
+     data[[3]] <- rvector(n = scale * 10000, ...)
+     data[[4]] <- rvector(n = scale * 1e+05, ...)
+     data[[5]] <- rvector(n = scale * 1e+06, ...)
+     names(data) <- sprintf("n = %d", sapply(data, FUN = length))
+     data
+ }
> data <- rvectors(mode = mode)
> data <- data[1:4]
```

### Results

### n = 1000 vector

#### All elements
```r
> x <- data[["n = 1000"]]
> stats <- microbenchmark(varDiff = varDiff(x), var = var(x), diff = diff(x), unit = "ms")
```

_Table: Benchmarking of varDiff(), var() and diff() on double+n = 1000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr    |      min|        lq|      mean|    median|        uq|      max|
|:--|:-------|--------:|---------:|---------:|---------:|---------:|--------:|
|2  |var     | 0.014357| 0.0151305| 0.0163587| 0.0156745| 0.0162965| 0.052366|
|3  |diff    | 0.015044| 0.0162720| 0.0172683| 0.0168995| 0.0174570| 0.043324|
|1  |varDiff | 0.021199| 0.0223960| 0.0236308| 0.0231905| 0.0241300| 0.045711|


|   |expr    |      min|       lq|    mean|   median|       uq|       max|
|:--|:-------|--------:|--------:|-------:|--------:|--------:|---------:|
|2  |var     | 1.000000| 1.000000| 1.00000| 1.000000| 1.000000| 1.0000000|
|3  |diff    | 1.047851| 1.075444| 1.05560| 1.078152| 1.071212| 0.8273307|
|1  |varDiff | 1.476562| 1.480189| 1.44454| 1.479505| 1.480686| 0.8729137|

_Figure: Benchmarking of varDiff(), var() and diff() on double+n = 1000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/varDiff,double,n=1000,benchmark.png)

### n = 10000 vector

#### All elements
```r
> x <- data[["n = 10000"]]
> stats <- microbenchmark(varDiff = varDiff(x), var = var(x), diff = diff(x), unit = "ms")
```

_Table: Benchmarking of varDiff(), var() and diff() on double+n = 10000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr    |      min|        lq|      mean|    median|        uq|      max|
|:--|:-------|--------:|---------:|---------:|---------:|---------:|--------:|
|2  |var     | 0.049284| 0.0508155| 0.0543732| 0.0530760| 0.0573315| 0.074749|
|1  |varDiff | 0.071503| 0.0723495| 0.0798305| 0.0763455| 0.0842170| 0.146072|
|3  |diff    | 0.066123| 0.0717585| 0.0806468| 0.0809885| 0.0860090| 0.115138|


|   |expr    |      min|       lq|     mean|   median|       uq|      max|
|:--|:-------|--------:|--------:|--------:|--------:|--------:|--------:|
|2  |var     | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|1  |varDiff | 1.450836| 1.423768| 1.468196| 1.438419| 1.468948| 1.954167|
|3  |diff    | 1.341673| 1.412138| 1.483208| 1.525897| 1.500205| 1.540328|

_Figure: Benchmarking of varDiff(), var() and diff() on double+n = 10000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/varDiff,double,n=10000,benchmark.png)

### n = 100000 vector

#### All elements
```r
> x <- data[["n = 100000"]]
> stats <- microbenchmark(varDiff = varDiff(x), var = var(x), diff = diff(x), unit = "ms")
```

_Table: Benchmarking of varDiff(), var() and diff() on double+n = 100000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr    |      min|       lq|      mean|    median|        uq|      max|
|:--|:-------|--------:|--------:|---------:|---------:|---------:|--------:|
|2  |var     | 0.318096| 0.321040| 0.3634486| 0.3499520| 0.3888045| 0.562683|
|1  |varDiff | 0.464472| 0.502048| 0.5917570| 0.5544725| 0.6843480| 0.873367|
|3  |diff    | 0.506269| 0.562587| 1.0449393| 0.6278750| 1.6096700| 6.902683|


|   |expr    |      min|       lq|     mean|   median|       uq|       max|
|:--|:-------|--------:|--------:|--------:|--------:|--------:|---------:|
|2  |var     | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|  1.000000|
|1  |varDiff | 1.460163| 1.563818| 1.628172| 1.584424| 1.760134|  1.552148|
|3  |diff    | 1.591560| 1.752389| 2.875067| 1.794175| 4.140050| 12.267445|

_Figure: Benchmarking of varDiff(), var() and diff() on double+n = 100000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/varDiff,double,n=100000,benchmark.png)

### n = 1000000 vector

#### All elements
```r
> x <- data[["n = 1000000"]]
> stats <- microbenchmark(varDiff = varDiff(x), var = var(x), diff = diff(x), unit = "ms")
```

_Table: Benchmarking of varDiff(), var() and diff() on double+n = 1000000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr    |      min|       lq|      mean|   median|        uq|        max|
|:--|:-------|--------:|--------:|---------:|--------:|---------:|----------:|
|2  |var     | 3.683399| 4.114583|  4.294322| 4.324982|  4.468257|   4.980643|
|1  |varDiff | 5.189352| 5.912148| 10.329994| 6.173566|  6.437409| 380.291779|
|3  |diff    | 6.836214| 7.286480| 10.141220| 7.588775| 13.534192|  27.061648|


|   |expr    |      min|       lq|     mean|   median|       uq|       max|
|:--|:-------|--------:|--------:|--------:|--------:|--------:|---------:|
|2  |var     | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|  1.000000|
|1  |varDiff | 1.408849| 1.436877| 2.405500| 1.427420| 1.440698| 76.353953|
|3  |diff    | 1.855953| 1.770892| 2.361541| 1.754637| 3.028964|  5.433364|

_Figure: Benchmarking of varDiff(), var() and diff() on double+n = 1000000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/varDiff,double,n=1000000,benchmark.png)



## Appendix

### Session information
```r
R version 4.1.1 Patched (2021-08-10 r80727)
Platform: x86_64-pc-linux-gnu (64-bit)
Running under: Ubuntu 18.04.5 LTS

Matrix products: default
BLAS:   /home/hb/software/R-devel/R-4-1-branch/lib/R/lib/libRblas.so
LAPACK: /home/hb/software/R-devel/R-4-1-branch/lib/R/lib/libRlapack.so

locale:
 [1] LC_CTYPE=en_US.UTF-8       LC_NUMERIC=C              
 [3] LC_TIME=en_US.UTF-8        LC_COLLATE=en_US.UTF-8    
 [5] LC_MONETARY=en_US.UTF-8    LC_MESSAGES=en_US.UTF-8   
 [7] LC_PAPER=en_US.UTF-8       LC_NAME=C                 
 [9] LC_ADDRESS=C               LC_TELEPHONE=C            
[11] LC_MEASUREMENT=en_US.UTF-8 LC_IDENTIFICATION=C       

attached base packages:
[1] stats     graphics  grDevices utils     datasets  methods   base     

other attached packages:
[1] microbenchmark_1.4-7   matrixStats_0.60.1     ggplot2_3.3.5         
[4] knitr_1.33             R.devices_2.17.0       R.utils_2.10.1        
[7] R.oo_1.24.0            R.methodsS3_1.8.1-9001 history_0.0.1-9000    

loaded via a namespace (and not attached):
 [1] Biobase_2.52.0          httr_1.4.2              splines_4.1.1          
 [4] bit64_4.0.5             network_1.17.1          assertthat_0.2.1       
 [7] highr_0.9               stats4_4.1.1            blob_1.2.2             
[10] GenomeInfoDbData_1.2.6  robustbase_0.93-8       pillar_1.6.2           
[13] RSQLite_2.2.8           lattice_0.20-44         glue_1.4.2             
[16] digest_0.6.27           XVector_0.32.0          colorspace_2.0-2       
[19] Matrix_1.3-4            XML_3.99-0.7            pkgconfig_2.0.3        
[22] zlibbioc_1.38.0         genefilter_1.74.0       purrr_0.3.4            
[25] ergm_4.1.2              xtable_1.8-4            scales_1.1.1           
[28] tibble_3.1.4            annotate_1.70.0         KEGGREST_1.32.0        
[31] farver_2.1.0            generics_0.1.0          IRanges_2.26.0         
[34] ellipsis_0.3.2          cachem_1.0.6            withr_2.4.2            
[37] BiocGenerics_0.38.0     mime_0.11               survival_3.2-13        
[40] magrittr_2.0.1          crayon_1.4.1            statnet.common_4.5.0   
[43] memoise_2.0.0           laeken_0.5.1            fansi_0.5.0            
[46] R.cache_0.15.0          MASS_7.3-54             R.rsp_0.44.0           
[49] progressr_0.8.0         tools_4.1.1             lifecycle_1.0.0        
[52] S4Vectors_0.30.0        trust_0.1-8             munsell_0.5.0          
[55] tabby_0.0.1-9001        AnnotationDbi_1.54.1    Biostrings_2.60.2      
[58] compiler_4.1.1          GenomeInfoDb_1.28.1     rlang_0.4.11           
[61] grid_4.1.1              RCurl_1.98-1.4          cwhmisc_6.6            
[64] rappdirs_0.3.3          startup_0.15.0          labeling_0.4.2         
[67] bitops_1.0-7            base64enc_0.1-3         boot_1.3-28            
[70] gtable_0.3.0            DBI_1.1.1               markdown_1.1           
[73] R6_2.5.1                lpSolveAPI_5.5.2.0-17.7 rle_0.9.2              
[76] dplyr_1.0.7             fastmap_1.1.0           bit_4.0.4              
[79] utf8_1.2.2              parallel_4.1.1          Rcpp_1.0.7             
[82] vctrs_0.3.8             png_0.1-7               DEoptimR_1.0-9         
[85] tidyselect_1.1.1        xfun_0.25               coda_0.19-4            
```
Total processing time was 13.46 secs.


### Reproducibility
To reproduce this report, do:
```r
html <- matrixStats:::benchmark('varDiff')
```

[RSP]: https://cran.r-project.org/package=R.rsp
[matrixStats]: https://cran.r-project.org/package=matrixStats

[StackOverflow:colMins?]: https://stackoverflow.com/questions/13676878 "Stack Overflow: fastest way to get Min from every column in a matrix?"
[StackOverflow:colSds?]: https://stackoverflow.com/questions/17549762 "Stack Overflow: Is there such 'colsd' in R?"
[StackOverflow:rowProds?]: https://stackoverflow.com/questions/20198801/ "Stack Overflow: Row product of matrix and column sum of matrix"

---------------------------------------
Copyright Henrik Bengtsson. Last updated on 2021-08-25 18:38:40 (+0200 UTC). Powered by [RSP].

<script>
 var link = document.createElement('link');
 link.rel = 'icon';
 link.href = "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAMAAABEpIrGAAAA21BMVEUAAAAAAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8BAf4CAv0DA/wdHeIeHuEfH+AgIN8hId4lJdomJtknJ9g+PsE/P8BAQL9yco10dIt1dYp3d4h4eIeVlWqWlmmXl2iYmGeZmWabm2Tn5xjo6Bfp6Rb39wj4+Af//wA2M9hbAAAASXRSTlMAAQIJCgsMJSYnKD4/QGRlZmhpamtsbautrrCxuru8y8zN5ebn6Pn6+///////////////////////////////////////////LsUNcQAAAS9JREFUOI29k21XgkAQhVcFytdSMqMETU26UVqGmpaiFbL//xc1cAhhwVNf6n5i5z67M2dmYOyfJZUqlVLhkKucG7cgmUZTybDz6g0iDeq51PUr37Ds2cy2/C9NeES5puDjxuUk1xnToZsg8pfA3avHQ3lLIi7iWRrkv/OYtkScxBIMgDee0ALoyxHQBJ68JLCjOtQIMIANF7QG9G9fNnHvisCHBVMKgSJgiz7nE+AoBKrAPA3MgepvgR9TSCasrCKH0eB1wBGBFdCO+nAGjMVGPcQb5bd6mQRegN6+1axOs9nGfYcCtfi4NQosdtH7dB+txFIpXQqN1p9B/asRHToyS0jRgpV7nk4nwcq1BJ+x3Gl/v7S9Wmpp/aGquum7w3ZDyrADFYrl8vHBH+ev9AUASW1dmU4h4wAAAABJRU5ErkJggg=="
 document.getElementsByTagName('head')[0].appendChild(link);
</script>



