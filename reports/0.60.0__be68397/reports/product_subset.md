





[matrixStats]: Benchmark report

---------------------------------------



# product() benchmarks on subsetted computation

This report benchmark the performance of product() on subsetted computation.


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
> data <- data[1:4]
```

## Results

### n = 1000 vector

```r
> x <- data[["n = 1000"]]
> idxs <- sample.int(length(x), size = length(x) * 0.7)
> x_S <- x[idxs]
> gc()
           used  (Mb) gc trigger  (Mb) max used  (Mb)
Ncells  5284339 282.3   10014072 534.9 10014072 534.9
Vcells 26102040 199.2   53036220 404.7 90959857 694.0
> stats <- microbenchmark(product_x_S = product(x_S, na.rm = FALSE), `product(x, idxs)` = product(x, 
+     idxs = idxs, na.rm = FALSE), `product(x[idxs])` = product(x[idxs], na.rm = FALSE), unit = "ms")
```

_Table: Benchmarking of product_x_S(), product(x, idxs)() and product(x[idxs])() on n = 1000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr             |      min|        lq|      mean|    median|        uq|      max|
|:--|:----------------|--------:|---------:|---------:|---------:|---------:|--------:|
|1  |product_x_S      | 0.021505| 0.0226665| 0.0232906| 0.0233025| 0.0237565| 0.030386|
|3  |product(x[idxs]) | 0.024060| 0.0252895| 0.0262169| 0.0258975| 0.0264675| 0.048788|
|2  |product(x, idxs) | 0.028183| 0.0291450| 0.0297966| 0.0297745| 0.0303755| 0.033803|


|   |expr             |      min|       lq|     mean|   median|       uq|      max|
|:--|:----------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |product_x_S      | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|3  |product(x[idxs]) | 1.118810| 1.115721| 1.125644| 1.111361| 1.114116| 1.605608|
|2  |product(x, idxs) | 1.310532| 1.285818| 1.279339| 1.277738| 1.278619| 1.112453|

_Figure: Benchmarking of product_x_S(), product(x, idxs)() and product(x[idxs])() on n = 1000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/product_x_S,n=1000,benchmark.png)

### n = 10000 vector

```r
> x <- data[["n = 10000"]]
> idxs <- sample.int(length(x), size = length(x) * 0.7)
> x_S <- x[idxs]
> gc()
           used  (Mb) gc trigger  (Mb) max used  (Mb)
Ncells  5281286 282.1   10014072 534.9 10014072 534.9
Vcells 10971130  83.8   42428976 323.8 90959857 694.0
> stats <- microbenchmark(product_x_S = product(x_S, na.rm = FALSE), `product(x, idxs)` = product(x, 
+     idxs = idxs, na.rm = FALSE), `product(x[idxs])` = product(x[idxs], na.rm = FALSE), unit = "ms")
```

_Table: Benchmarking of product_x_S(), product(x, idxs)() and product(x[idxs])() on n = 10000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr             |      min|        lq|      mean|    median|        uq|      max|
|:--|:----------------|--------:|---------:|---------:|---------:|---------:|--------:|
|1  |product_x_S      | 0.161022| 0.1702040| 0.1996902| 0.1945270| 0.2185675| 0.267262|
|3  |product(x[idxs]) | 0.175093| 0.1818295| 0.2124554| 0.2028875| 0.2301930| 0.333496|
|2  |product(x, idxs) | 0.191405| 0.2002220| 0.2390451| 0.2336930| 0.2701410| 0.328458|


|   |expr             |      min|       lq|     mean|   median|       uq|      max|
|:--|:----------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |product_x_S      | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|3  |product(x[idxs]) | 1.087386| 1.068303| 1.063925| 1.042979| 1.053190| 1.247824|
|2  |product(x, idxs) | 1.188689| 1.176365| 1.197080| 1.201340| 1.235961| 1.228974|

_Figure: Benchmarking of product_x_S(), product(x, idxs)() and product(x[idxs])() on n = 10000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/product_x_S,n=10000,benchmark.png)

### n = 100000 vector

```r
> x <- data[["n = 100000"]]
> idxs <- sample.int(length(x), size = length(x) * 0.7)
> x_S <- x[idxs]
> gc()
           used  (Mb) gc trigger  (Mb) max used  (Mb)
Ncells  5281358 282.1   10014072 534.9 10014072 534.9
Vcells 11066190  84.5   33943181 259.0 90959857 694.0
> stats <- microbenchmark(product_x_S = product(x_S, na.rm = FALSE), `product(x, idxs)` = product(x, 
+     idxs = idxs, na.rm = FALSE), `product(x[idxs])` = product(x[idxs], na.rm = FALSE), unit = "ms")
```

_Table: Benchmarking of product_x_S(), product(x, idxs)() and product(x[idxs])() on n = 100000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr             |      min|       lq|     mean|   median|       uq|      max|
|:--|:----------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |product_x_S      | 1.618102| 1.797979| 1.836850| 1.807363| 1.856732| 2.655251|
|3  |product(x[idxs]) | 1.805745| 2.000580| 2.042931| 2.008487| 2.027536| 3.085068|
|2  |product(x, idxs) | 2.339383| 2.608563| 2.656796| 2.615314| 2.689261| 3.412401|


|   |expr             |      min|       lq|     mean|   median|       uq|      max|
|:--|:----------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |product_x_S      | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|3  |product(x[idxs]) | 1.115965| 1.112682| 1.112192| 1.111280| 1.091991| 1.161874|
|2  |product(x, idxs) | 1.445757| 1.450830| 1.446387| 1.447033| 1.448383| 1.285152|

_Figure: Benchmarking of product_x_S(), product(x, idxs)() and product(x[idxs])() on n = 100000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/product_x_S,n=100000,benchmark.png)

### n = 1000000 vector

```r
> x <- data[["n = 1000000"]]
> idxs <- sample.int(length(x), size = length(x) * 0.7)
> x_S <- x[idxs]
> gc()
           used  (Mb) gc trigger  (Mb) max used  (Mb)
Ncells  5281430 282.1   10014072 534.9 10014072 534.9
Vcells 12011239  91.7   33943181 259.0 90959857 694.0
> stats <- microbenchmark(product_x_S = product(x_S, na.rm = FALSE), `product(x, idxs)` = product(x, 
+     idxs = idxs, na.rm = FALSE), `product(x[idxs])` = product(x[idxs], na.rm = FALSE), unit = "ms")
```

_Table: Benchmarking of product_x_S(), product(x, idxs)() and product(x[idxs])() on n = 1000000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr             |      min|       lq|     mean|   median|       uq|      max|
|:--|:----------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |product_x_S      | 16.33600| 17.40443| 19.19524| 18.54330| 21.47322| 24.04240|
|3  |product(x[idxs]) | 23.69342| 26.69620| 28.04704| 27.47381| 29.68485| 37.98521|
|2  |product(x, idxs) | 48.84762| 53.29354| 57.11390| 55.82199| 59.34093| 74.87089|


|   |expr             |      min|       lq|     mean|   median|       uq|      max|
|:--|:----------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |product_x_S      | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|3  |product(x[idxs]) | 1.450381| 1.533874| 1.461145| 1.481603| 1.382413| 1.579926|
|2  |product(x, idxs) | 2.990183| 3.062068| 2.975420| 3.010359| 2.763486| 3.114119|

_Figure: Benchmarking of product_x_S(), product(x, idxs)() and product(x[idxs])() on n = 1000000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/product_x_S,n=1000000,benchmark.png)



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
Total processing time was 15.37 secs.


### Reproducibility
To reproduce this report, do:
```r
html <- matrixStats:::benchmark('product_subset')
```

[RSP]: https://cran.r-project.org/package=R.rsp
[matrixStats]: https://cran.r-project.org/package=matrixStats

[StackOverflow:colMins?]: https://stackoverflow.com/questions/13676878 "Stack Overflow: fastest way to get Min from every column in a matrix?"
[StackOverflow:colSds?]: https://stackoverflow.com/questions/17549762 "Stack Overflow: Is there such 'colsd' in R?"
[StackOverflow:rowProds?]: https://stackoverflow.com/questions/20198801/ "Stack Overflow: Row product of matrix and column sum of matrix"

---------------------------------------
Copyright Dongcan Jiang. Last updated on 2021-08-25 18:32:46 (+0200 UTC). Powered by [RSP].

<script>
 var link = document.createElement('link');
 link.rel = 'icon';
 link.href = "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAMAAABEpIrGAAAA21BMVEUAAAAAAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8BAf4CAv0DA/wdHeIeHuEfH+AgIN8hId4lJdomJtknJ9g+PsE/P8BAQL9yco10dIt1dYp3d4h4eIeVlWqWlmmXl2iYmGeZmWabm2Tn5xjo6Bfp6Rb39wj4+Af//wA2M9hbAAAASXRSTlMAAQIJCgsMJSYnKD4/QGRlZmhpamtsbautrrCxuru8y8zN5ebn6Pn6+///////////////////////////////////////////LsUNcQAAAS9JREFUOI29k21XgkAQhVcFytdSMqMETU26UVqGmpaiFbL//xc1cAhhwVNf6n5i5z67M2dmYOyfJZUqlVLhkKucG7cgmUZTybDz6g0iDeq51PUr37Ds2cy2/C9NeES5puDjxuUk1xnToZsg8pfA3avHQ3lLIi7iWRrkv/OYtkScxBIMgDee0ALoyxHQBJ68JLCjOtQIMIANF7QG9G9fNnHvisCHBVMKgSJgiz7nE+AoBKrAPA3MgepvgR9TSCasrCKH0eB1wBGBFdCO+nAGjMVGPcQb5bd6mQRegN6+1axOs9nGfYcCtfi4NQosdtH7dB+txFIpXQqN1p9B/asRHToyS0jRgpV7nk4nwcq1BJ+x3Gl/v7S9Wmpp/aGquum7w3ZDyrADFYrl8vHBH+ev9AUASW1dmU4h4wAAAABJRU5ErkJggg=="
 document.getElementsByTagName('head')[0].appendChild(link);
</script>



