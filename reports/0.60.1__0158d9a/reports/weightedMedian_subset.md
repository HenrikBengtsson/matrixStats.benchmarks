




[matrixStats]: Benchmark report

---------------------------------------



# weightedMedian() benchmarks on subsetted computation

This report benchmark the performance of weightedMedian() on subsetted computation.


## Data
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
> data <- rvectors(mode = "double")
> data <- data[1:3]
```

## Results

### n = 1000 vector

```r
> x <- data[["n = 1000"]]
> idxs <- sample.int(length(x), size = length(x) * 0.7)
> x_S <- x[idxs]
> w <- runif(length(x))
> w_S <- x[idxs]
> gc()
           used  (Mb) gc trigger  (Mb)  max used  (Mb)
Ncells  5363024 286.5    8529671 455.6   8529671 455.6
Vcells 12570868  96.0   39910282 304.5 101881463 777.3
> stats <- microbenchmark(weightedMedian_x_w_S = weightedMedian(x_S, w = w_S, ties = "mean", na.rm = FALSE), 
+     `weightedMedian(x, w, idxs)` = weightedMedian(x, w = w, idxs = idxs, ties = "mean", na.rm = FALSE), 
+     `weightedMedian(x[idxs], w[idxs])` = weightedMedian(x[idxs], w = w[idxs], ties = "mean", na.rm = FALSE), 
+     unit = "ms")
```

_Table: Benchmarking of weightedMedian_x_w_S(), weightedMedian(x, w, idxs)() and weightedMedian(x[idxs], w[idxs])() on n = 1000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr                             |      min|        lq|      mean|    median|        uq|      max|
|:--|:--------------------------------|--------:|---------:|---------:|---------:|---------:|--------:|
|1  |weightedMedian_x_w_S             | 0.022068| 0.0262415| 0.0278228| 0.0274145| 0.0288025| 0.047283|
|2  |weightedMedian(x, w, idxs)       | 0.038439| 0.0425555| 0.0450344| 0.0443435| 0.0461070| 0.086493|
|3  |weightedMedian(x[idxs], w[idxs]) | 0.040360| 0.0436655| 0.0460851| 0.0457695| 0.0479970| 0.061564|


|   |expr                             |      min|       lq|     mean|   median|       uq|      max|
|:--|:--------------------------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |weightedMedian_x_w_S             | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|2  |weightedMedian(x, w, idxs)       | 1.741843| 1.621687| 1.618615| 1.617520| 1.600799| 1.829262|
|3  |weightedMedian(x[idxs], w[idxs]) | 1.828893| 1.663986| 1.656380| 1.669536| 1.666418| 1.302032|

_Figure: Benchmarking of weightedMedian_x_w_S(), weightedMedian(x, w, idxs)() and weightedMedian(x[idxs], w[idxs])() on n = 1000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/weightedMedian_x_w_S,n=1000,benchmark.png)

### n = 10000 vector

```r
> x <- data[["n = 10000"]]
> idxs <- sample.int(length(x), size = length(x) * 0.7)
> x_S <- x[idxs]
> w <- runif(length(x))
> w_S <- x[idxs]
> gc()
           used  (Mb) gc trigger  (Mb)  max used  (Mb)
Ncells  5350565 285.8    8529671 455.6   8529671 455.6
Vcells 10426269  79.6   39910282 304.5 101881463 777.3
> stats <- microbenchmark(weightedMedian_x_w_S = weightedMedian(x_S, w = w_S, ties = "mean", na.rm = FALSE), 
+     `weightedMedian(x, w, idxs)` = weightedMedian(x, w = w, idxs = idxs, ties = "mean", na.rm = FALSE), 
+     `weightedMedian(x[idxs], w[idxs])` = weightedMedian(x[idxs], w = w[idxs], ties = "mean", na.rm = FALSE), 
+     unit = "ms")
```

_Table: Benchmarking of weightedMedian_x_w_S(), weightedMedian(x, w, idxs)() and weightedMedian(x[idxs], w[idxs])() on n = 10000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr                             |      min|        lq|      mean|    median|       uq|      max|
|:--|:--------------------------------|--------:|---------:|---------:|---------:|--------:|--------:|
|1  |weightedMedian_x_w_S             | 0.242221| 0.2476960| 0.2750178| 0.2569040| 0.291548| 0.418357|
|2  |weightedMedian(x, w, idxs)       | 0.407897| 0.4132000| 0.4500956| 0.4246210| 0.448941| 0.687807|
|3  |weightedMedian(x[idxs], w[idxs]) | 0.413669| 0.4223365| 0.4799637| 0.4393675| 0.522597| 0.756214|


|   |expr                             |      min|       lq|     mean|   median|       uq|      max|
|:--|:--------------------------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |weightedMedian_x_w_S             | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|2  |weightedMedian(x, w, idxs)       | 1.683987| 1.668174| 1.636605| 1.652839| 1.539853| 1.644067|
|3  |weightedMedian(x[idxs], w[idxs]) | 1.707816| 1.705060| 1.745209| 1.710240| 1.792490| 1.807581|

_Figure: Benchmarking of weightedMedian_x_w_S(), weightedMedian(x, w, idxs)() and weightedMedian(x[idxs], w[idxs])() on n = 10000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/weightedMedian_x_w_S,n=10000,benchmark.png)

### n = 100000 vector

```r
> x <- data[["n = 100000"]]
> idxs <- sample.int(length(x), size = length(x) * 0.7)
> x_S <- x[idxs]
> w <- runif(length(x))
> w_S <- x[idxs]
> gc()
           used  (Mb) gc trigger  (Mb)  max used  (Mb)
Ncells  5350637 285.8    8529671 455.6   8529671 455.6
Vcells 10674329  81.5   39910282 304.5 101881463 777.3
> stats <- microbenchmark(weightedMedian_x_w_S = weightedMedian(x_S, w = w_S, ties = "mean", na.rm = FALSE), 
+     `weightedMedian(x, w, idxs)` = weightedMedian(x, w = w, idxs = idxs, ties = "mean", na.rm = FALSE), 
+     `weightedMedian(x[idxs], w[idxs])` = weightedMedian(x[idxs], w = w[idxs], ties = "mean", na.rm = FALSE), 
+     unit = "ms")
```

_Table: Benchmarking of weightedMedian_x_w_S(), weightedMedian(x, w, idxs)() and weightedMedian(x[idxs], w[idxs])() on n = 100000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr                             |      min|       lq|     mean|   median|       uq|      max|
|:--|:--------------------------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |weightedMedian_x_w_S             | 2.832098| 3.054331| 3.122695| 3.086237| 3.116154| 4.669408|
|2  |weightedMedian(x, w, idxs)       | 5.086733| 5.522982| 5.662233| 5.658106| 5.748962| 7.060010|
|3  |weightedMedian(x[idxs], w[idxs]) | 5.088597| 5.528759| 5.769173| 5.755913| 5.919936| 8.074829|


|   |expr                             |      min|       lq|     mean|   median|       uq|      max|
|:--|:--------------------------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |weightedMedian_x_w_S             | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|2  |weightedMedian(x, w, idxs)       | 1.796101| 1.808246| 1.813252| 1.833335| 1.844890| 1.511971|
|3  |weightedMedian(x[idxs], w[idxs]) | 1.796759| 1.810137| 1.847498| 1.865026| 1.899757| 1.729305|

_Figure: Benchmarking of weightedMedian_x_w_S(), weightedMedian(x, w, idxs)() and weightedMedian(x[idxs], w[idxs])() on n = 100000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/weightedMedian_x_w_S,n=100000,benchmark.png)


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
Total processing time was 4.78 secs.


### Reproducibility
To reproduce this report, do:
```r
html <- matrixStats:::benchmark('weightedMedian_subset')
```

[RSP]: https://cran.r-project.org/package=R.rsp
[matrixStats]: https://cran.r-project.org/package=matrixStats

[StackOverflow:colMins?]: https://stackoverflow.com/questions/13676878 "Stack Overflow: fastest way to get Min from every column in a matrix?"
[StackOverflow:colSds?]: https://stackoverflow.com/questions/17549762 "Stack Overflow: Is there such 'colsd' in R?"
[StackOverflow:rowProds?]: https://stackoverflow.com/questions/20198801/ "Stack Overflow: Row product of matrix and column sum of matrix"

---------------------------------------
Copyright Dongcan Jiang. Last updated on 2021-08-25 19:32:20 (+0200 UTC). Powered by [RSP].

<script>
 var link = document.createElement('link');
 link.rel = 'icon';
 link.href = "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAMAAABEpIrGAAAA21BMVEUAAAAAAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8BAf4CAv0DA/wdHeIeHuEfH+AgIN8hId4lJdomJtknJ9g+PsE/P8BAQL9yco10dIt1dYp3d4h4eIeVlWqWlmmXl2iYmGeZmWabm2Tn5xjo6Bfp6Rb39wj4+Af//wA2M9hbAAAASXRSTlMAAQIJCgsMJSYnKD4/QGRlZmhpamtsbautrrCxuru8y8zN5ebn6Pn6+///////////////////////////////////////////LsUNcQAAAS9JREFUOI29k21XgkAQhVcFytdSMqMETU26UVqGmpaiFbL//xc1cAhhwVNf6n5i5z67M2dmYOyfJZUqlVLhkKucG7cgmUZTybDz6g0iDeq51PUr37Ds2cy2/C9NeES5puDjxuUk1xnToZsg8pfA3avHQ3lLIi7iWRrkv/OYtkScxBIMgDee0ALoyxHQBJ68JLCjOtQIMIANF7QG9G9fNnHvisCHBVMKgSJgiz7nE+AoBKrAPA3MgepvgR9TSCasrCKH0eB1wBGBFdCO+nAGjMVGPcQb5bd6mQRegN6+1axOs9nGfYcCtfi4NQosdtH7dB+txFIpXQqN1p9B/asRHToyS0jRgpV7nk4nwcq1BJ+x3Gl/v7S9Wmpp/aGquum7w3ZDyrADFYrl8vHBH+ev9AUASW1dmU4h4wAAAABJRU5ErkJggg=="
 document.getElementsByTagName('head')[0].appendChild(link);
</script>



