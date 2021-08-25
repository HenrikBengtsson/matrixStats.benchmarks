




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
           used  (Mb) gc trigger  (Mb) max used  (Mb)
Ncells  5365471 286.6    7916910 422.9  7916910 422.9
Vcells 12591581  96.1   39038428 297.9 94934136 724.3
> stats <- microbenchmark(weightedMedian_x_w_S = weightedMedian(x_S, w = w_S, ties = "mean", na.rm = FALSE), 
+     `weightedMedian(x, w, idxs)` = weightedMedian(x, w = w, idxs = idxs, ties = "mean", na.rm = FALSE), 
+     `weightedMedian(x[idxs], w[idxs])` = weightedMedian(x[idxs], w = w[idxs], ties = "mean", na.rm = FALSE), 
+     unit = "ms")
```

_Table: Benchmarking of weightedMedian_x_w_S(), weightedMedian(x, w, idxs)() and weightedMedian(x[idxs], w[idxs])() on n = 1000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr                             |      min|        lq|      mean|    median|        uq|      max|
|:--|:--------------------------------|--------:|---------:|---------:|---------:|---------:|--------:|
|1  |weightedMedian_x_w_S             | 0.025993| 0.0296005| 0.0311789| 0.0308535| 0.0322230| 0.047863|
|2  |weightedMedian(x, w, idxs)       | 0.039677| 0.0421460| 0.0442247| 0.0431995| 0.0448555| 0.099545|
|3  |weightedMedian(x[idxs], w[idxs]) | 0.043383| 0.0454240| 0.0482020| 0.0468850| 0.0490145| 0.080744|


|   |expr                             |      min|       lq|     mean|   median|       uq|      max|
|:--|:--------------------------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |weightedMedian_x_w_S             | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|2  |weightedMedian(x, w, idxs)       | 1.526449| 1.423827| 1.418417| 1.400149| 1.392034| 2.079790|
|3  |weightedMedian(x[idxs], w[idxs]) | 1.669026| 1.534569| 1.545980| 1.519601| 1.521103| 1.686982|

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
           used  (Mb) gc trigger  (Mb) max used  (Mb)
Ncells  5362619 286.4    7916910 422.9  7916910 422.9
Vcells 10478946  80.0   39038428 297.9 94934136 724.3
> stats <- microbenchmark(weightedMedian_x_w_S = weightedMedian(x_S, w = w_S, ties = "mean", na.rm = FALSE), 
+     `weightedMedian(x, w, idxs)` = weightedMedian(x, w = w, idxs = idxs, ties = "mean", na.rm = FALSE), 
+     `weightedMedian(x[idxs], w[idxs])` = weightedMedian(x[idxs], w = w[idxs], ties = "mean", na.rm = FALSE), 
+     unit = "ms")
```

_Table: Benchmarking of weightedMedian_x_w_S(), weightedMedian(x, w, idxs)() and weightedMedian(x[idxs], w[idxs])() on n = 10000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr                             |      min|       lq|      mean|   median|        uq|      max|
|:--|:--------------------------------|--------:|--------:|---------:|--------:|---------:|--------:|
|1  |weightedMedian_x_w_S             | 0.229462| 0.234522| 0.2660686| 0.238139| 0.2971940| 0.390752|
|2  |weightedMedian(x, w, idxs)       | 0.392851| 0.396198| 0.4424426| 0.402958| 0.4701835| 0.669262|
|3  |weightedMedian(x[idxs], w[idxs]) | 0.405238| 0.409998| 0.4850652| 0.422549| 0.5320350| 0.787552|


|   |expr                             |      min|       lq|     mean|   median|       uq|      max|
|:--|:--------------------------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |weightedMedian_x_w_S             | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|2  |weightedMedian(x, w, idxs)       | 1.712052| 1.689385| 1.662889| 1.692113| 1.582076| 1.712754|
|3  |weightedMedian(x[idxs], w[idxs]) | 1.766035| 1.748228| 1.823083| 1.774380| 1.790194| 2.015478|

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
           used  (Mb) gc trigger  (Mb) max used  (Mb)
Ncells  5362691 286.4    7916910 422.9  7916910 422.9
Vcells 10727006  81.9   39038428 297.9 94934136 724.3
> stats <- microbenchmark(weightedMedian_x_w_S = weightedMedian(x_S, w = w_S, ties = "mean", na.rm = FALSE), 
+     `weightedMedian(x, w, idxs)` = weightedMedian(x, w = w, idxs = idxs, ties = "mean", na.rm = FALSE), 
+     `weightedMedian(x[idxs], w[idxs])` = weightedMedian(x[idxs], w = w[idxs], ties = "mean", na.rm = FALSE), 
+     unit = "ms")
```

_Table: Benchmarking of weightedMedian_x_w_S(), weightedMedian(x, w, idxs)() and weightedMedian(x[idxs], w[idxs])() on n = 100000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr                             |      min|       lq|     mean|   median|       uq|      max|
|:--|:--------------------------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |weightedMedian_x_w_S             | 2.720068| 2.735365| 2.815580| 2.746850| 2.768208| 4.629788|
|2  |weightedMedian(x, w, idxs)       | 4.895023| 4.938561| 5.062165| 4.983714| 5.079594| 6.634633|
|3  |weightedMedian(x[idxs], w[idxs]) | 4.984670| 5.080361| 5.375530| 5.206656| 5.393571| 8.634173|


|   |expr                             |      min|       lq|     mean|   median|       uq|      max|
|:--|:--------------------------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |weightedMedian_x_w_S             | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|2  |weightedMedian(x, w, idxs)       | 1.799596| 1.805449| 1.797912| 1.814338| 1.834976| 1.433032|
|3  |weightedMedian(x[idxs], w[idxs]) | 1.832553| 1.857288| 1.909209| 1.895501| 1.948398| 1.864918|

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
Total processing time was 4.74 secs.


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
Copyright Dongcan Jiang. Last updated on 2021-08-25 22:52:50 (+0200 UTC). Powered by [RSP].

<script>
 var link = document.createElement('link');
 link.rel = 'icon';
 link.href = "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAMAAABEpIrGAAAA21BMVEUAAAAAAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8BAf4CAv0DA/wdHeIeHuEfH+AgIN8hId4lJdomJtknJ9g+PsE/P8BAQL9yco10dIt1dYp3d4h4eIeVlWqWlmmXl2iYmGeZmWabm2Tn5xjo6Bfp6Rb39wj4+Af//wA2M9hbAAAASXRSTlMAAQIJCgsMJSYnKD4/QGRlZmhpamtsbautrrCxuru8y8zN5ebn6Pn6+///////////////////////////////////////////LsUNcQAAAS9JREFUOI29k21XgkAQhVcFytdSMqMETU26UVqGmpaiFbL//xc1cAhhwVNf6n5i5z67M2dmYOyfJZUqlVLhkKucG7cgmUZTybDz6g0iDeq51PUr37Ds2cy2/C9NeES5puDjxuUk1xnToZsg8pfA3avHQ3lLIi7iWRrkv/OYtkScxBIMgDee0ALoyxHQBJ68JLCjOtQIMIANF7QG9G9fNnHvisCHBVMKgSJgiz7nE+AoBKrAPA3MgepvgR9TSCasrCKH0eB1wBGBFdCO+nAGjMVGPcQb5bd6mQRegN6+1axOs9nGfYcCtfi4NQosdtH7dB+txFIpXQqN1p9B/asRHToyS0jRgpV7nk4nwcq1BJ+x3Gl/v7S9Wmpp/aGquum7w3ZDyrADFYrl8vHBH+ev9AUASW1dmU4h4wAAAABJRU5ErkJggg=="
 document.getElementsByTagName('head')[0].appendChild(link);
</script>



