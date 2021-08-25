





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
Ncells  5350371 285.8    7916910 422.9  7916910 422.9
Vcells 26574849 202.8   54892165 418.8 94934136 724.3
> stats <- microbenchmark(product_x_S = product(x_S, na.rm = FALSE), `product(x, idxs)` = product(x, 
+     idxs = idxs, na.rm = FALSE), `product(x[idxs])` = product(x[idxs], na.rm = FALSE), unit = "ms")
```

_Table: Benchmarking of product_x_S(), product(x, idxs)() and product(x[idxs])() on n = 1000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr             |      min|        lq|      mean|    median|        uq|      max|
|:--|:----------------|--------:|---------:|---------:|---------:|---------:|--------:|
|1  |product_x_S      | 0.018551| 0.0192720| 0.0198941| 0.0197205| 0.0202295| 0.034530|
|2  |product(x, idxs) | 0.019637| 0.0204445| 0.0213027| 0.0210520| 0.0218930| 0.028677|
|3  |product(x[idxs]) | 0.020544| 0.0216435| 0.0226630| 0.0222330| 0.0228465| 0.050459|


|   |expr             |      min|       lq|     mean|   median|       uq|       max|
|:--|:----------------|--------:|--------:|--------:|--------:|--------:|---------:|
|1  |product_x_S      | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.0000000|
|2  |product(x, idxs) | 1.058541| 1.060840| 1.070806| 1.067519| 1.082231| 0.8304952|
|3  |product(x[idxs]) | 1.107434| 1.123054| 1.139185| 1.127406| 1.129366| 1.4613090|

_Figure: Benchmarking of product_x_S(), product(x, idxs)() and product(x[idxs])() on n = 1000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/product_x_S,n=1000,benchmark.png)

### n = 10000 vector

```r
> x <- data[["n = 10000"]]
> idxs <- sample.int(length(x), size = length(x) * 0.7)
> x_S <- x[idxs]
> gc()
           used  (Mb) gc trigger  (Mb) max used  (Mb)
Ncells  5347786 285.7    7916910 422.9  7916910 422.9
Vcells 11445402  87.4   43913732 335.1 94934136 724.3
> stats <- microbenchmark(product_x_S = product(x_S, na.rm = FALSE), `product(x, idxs)` = product(x, 
+     idxs = idxs, na.rm = FALSE), `product(x[idxs])` = product(x[idxs], na.rm = FALSE), unit = "ms")
```

_Table: Benchmarking of product_x_S(), product(x, idxs)() and product(x[idxs])() on n = 10000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr             |      min|        lq|      mean|    median|        uq|      max|
|:--|:----------------|--------:|---------:|---------:|---------:|---------:|--------:|
|1  |product_x_S      | 0.153597| 0.1589205| 0.1889438| 0.1857690| 0.2083460| 0.256036|
|3  |product(x[idxs]) | 0.167638| 0.1726615| 0.2010916| 0.1930770| 0.2192160| 0.311540|
|2  |product(x, idxs) | 0.183204| 0.1894220| 0.2252754| 0.2187645| 0.2458025| 0.311680|


|   |expr             |      min|       lq|     mean|   median|       uq|      max|
|:--|:----------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |product_x_S      | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|3  |product(x[idxs]) | 1.091414| 1.086465| 1.064293| 1.039339| 1.052173| 1.216782|
|2  |product(x, idxs) | 1.192758| 1.191929| 1.192288| 1.177616| 1.179780| 1.217329|

_Figure: Benchmarking of product_x_S(), product(x, idxs)() and product(x[idxs])() on n = 10000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/product_x_S,n=10000,benchmark.png)

### n = 100000 vector

```r
> x <- data[["n = 100000"]]
> idxs <- sample.int(length(x), size = length(x) * 0.7)
> x_S <- x[idxs]
> gc()
           used  (Mb) gc trigger  (Mb) max used  (Mb)
Ncells  5347858 285.7    7916910 422.9  7916910 422.9
Vcells 11540462  88.1   35130986 268.1 94934136 724.3
> stats <- microbenchmark(product_x_S = product(x_S, na.rm = FALSE), `product(x, idxs)` = product(x, 
+     idxs = idxs, na.rm = FALSE), `product(x[idxs])` = product(x[idxs], na.rm = FALSE), unit = "ms")
```

_Table: Benchmarking of product_x_S(), product(x, idxs)() and product(x[idxs])() on n = 100000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr             |      min|       lq|     mean|   median|       uq|      max|
|:--|:----------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |product_x_S      | 1.549952| 1.688692| 1.730460| 1.727593| 1.733352| 2.548933|
|3  |product(x[idxs]) | 1.738329| 1.899376| 1.951108| 1.935016| 1.943423| 2.839429|
|2  |product(x, idxs) | 2.248668| 2.495837| 2.498071| 2.513803| 2.519142| 2.849638|


|   |expr             |      min|       lq|     mean|   median|       uq|      max|
|:--|:----------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |product_x_S      | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|3  |product(x[idxs]) | 1.121537| 1.124761| 1.127508| 1.120065| 1.121194| 1.113968|
|2  |product(x, idxs) | 1.450799| 1.477970| 1.443588| 1.455089| 1.453335| 1.117973|

_Figure: Benchmarking of product_x_S(), product(x, idxs)() and product(x[idxs])() on n = 100000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/product_x_S,n=100000,benchmark.png)

### n = 1000000 vector

```r
> x <- data[["n = 1000000"]]
> idxs <- sample.int(length(x), size = length(x) * 0.7)
> x_S <- x[idxs]
> gc()
           used  (Mb) gc trigger  (Mb) max used  (Mb)
Ncells  5347930 285.7    7916910 422.9  7916910 422.9
Vcells 12485511  95.3   35130986 268.1 94934136 724.3
> stats <- microbenchmark(product_x_S = product(x_S, na.rm = FALSE), `product(x, idxs)` = product(x, 
+     idxs = idxs, na.rm = FALSE), `product(x[idxs])` = product(x[idxs], na.rm = FALSE), unit = "ms")
```

_Table: Benchmarking of product_x_S(), product(x, idxs)() and product(x[idxs])() on n = 1000000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr             |      min|       lq|     mean|   median|       uq|      max|
|:--|:----------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |product_x_S      | 15.60263| 17.33577| 19.97094| 19.25093| 22.90886| 30.71439|
|3  |product(x[idxs]) | 24.81399| 28.14037| 30.92797| 30.11235| 33.43813| 47.27077|
|2  |product(x, idxs) | 50.91459| 58.90147| 65.89198| 64.07197| 71.18637| 95.78670|


|   |expr             |      min|       lq|     mean|   median|       uq|      max|
|:--|:----------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |product_x_S      | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|3  |product(x[idxs]) | 1.590372| 1.623255| 1.548649| 1.564203| 1.459616| 1.539043|
|2  |product(x, idxs) | 3.263205| 3.397684| 3.299392| 3.328254| 3.107373| 3.118626|

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
[1] microbenchmark_1.4-7   matrixStats_0.60.0     ggplot2_3.3.5         
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
[64] rstudioapi_0.13         rappdirs_0.3.3          startup_0.15.0-9000    
[67] labeling_0.4.2          bitops_1.0-7            base64enc_0.1-3        
[70] boot_1.3-28             gtable_0.3.0            DBI_1.1.1              
[73] markdown_1.1            R6_2.5.1                lpSolveAPI_5.5.2.0-17.7
[76] rle_0.9.2               dplyr_1.0.7             fastmap_1.1.0          
[79] bit_4.0.4               utf8_1.2.2              parallel_4.1.1         
[82] Rcpp_1.0.7              vctrs_0.3.8             png_0.1-7              
[85] DEoptimR_1.0-9          tidyselect_1.1.1        xfun_0.25              
[88] coda_0.19-4            
```
Total processing time was 16.47 secs.


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
Copyright Dongcan Jiang. Last updated on 2021-08-25 22:46:16 (+0200 UTC). Powered by [RSP].

<script>
 var link = document.createElement('link');
 link.rel = 'icon';
 link.href = "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAMAAABEpIrGAAAA21BMVEUAAAAAAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8BAf4CAv0DA/wdHeIeHuEfH+AgIN8hId4lJdomJtknJ9g+PsE/P8BAQL9yco10dIt1dYp3d4h4eIeVlWqWlmmXl2iYmGeZmWabm2Tn5xjo6Bfp6Rb39wj4+Af//wA2M9hbAAAASXRSTlMAAQIJCgsMJSYnKD4/QGRlZmhpamtsbautrrCxuru8y8zN5ebn6Pn6+///////////////////////////////////////////LsUNcQAAAS9JREFUOI29k21XgkAQhVcFytdSMqMETU26UVqGmpaiFbL//xc1cAhhwVNf6n5i5z67M2dmYOyfJZUqlVLhkKucG7cgmUZTybDz6g0iDeq51PUr37Ds2cy2/C9NeES5puDjxuUk1xnToZsg8pfA3avHQ3lLIi7iWRrkv/OYtkScxBIMgDee0ALoyxHQBJ68JLCjOtQIMIANF7QG9G9fNnHvisCHBVMKgSJgiz7nE+AoBKrAPA3MgepvgR9TSCasrCKH0eB1wBGBFdCO+nAGjMVGPcQb5bd6mQRegN6+1axOs9nGfYcCtfi4NQosdtH7dB+txFIpXQqN1p9B/asRHToyS0jRgpV7nk4nwcq1BJ+x3Gl/v7S9Wmpp/aGquum7w3ZDyrADFYrl8vHBH+ev9AUASW1dmU4h4wAAAABJRU5ErkJggg=="
 document.getElementsByTagName('head')[0].appendChild(link);
</script>



