




[matrixStats]: Benchmark report

---------------------------------------




# weightedMedian() benchmarks

This report benchmark the performance of weightedMedian() against alternative methods.

## Alternative methods

* apply() + limma::weighted.median()
* apply() + cwhmisc::w.median()
* apply() + laeken::weightedMedian()


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
> w <- runif(length(x))
> gc()
           used  (Mb) gc trigger  (Mb)  max used  (Mb)
Ncells  5399067 288.4    8529671 455.6   8529671 455.6
Vcells 10888970  83.1   39910282 304.5 101881463 777.3
> stats <- microbenchmark(weightedMedian = weightedMedian(x, w = w, ties = "mean", na.rm = FALSE), 
+     `limma::weighted.median` = limma_weighted.median(x, w = w, na.rm = FALSE), `cwhmisc::w.median` = cwhmisc_w.median(x, 
+         w = w), `laeken::weightedMedian` = laeken_weightedMedian(x, w = w), unit = "ms")
```

_Table: Benchmarking of weightedMedian(), limma::weighted.median(), cwhmisc::w.median() and laeken::weightedMedian() on n = 1000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr                   |      min|        lq|      mean|    median|        uq|      max|
|:--|:----------------------|--------:|---------:|---------:|---------:|---------:|--------:|
|1  |weightedMedian         | 0.052821| 0.0626815| 0.0679817| 0.0656180| 0.0707465| 0.104965|
|2  |limma::weighted.median | 0.079736| 0.0883770| 0.0975250| 0.0939640| 0.1042830| 0.200039|
|3  |cwhmisc::w.median      | 0.110723| 0.1210920| 0.1290402| 0.1257495| 0.1348620| 0.173337|
|4  |laeken::weightedMedian | 0.155514| 0.1722420| 0.1917443| 0.1816670| 0.1953360| 0.671221|


|   |expr                   |      min|       lq|     mean|   median|       uq|      max|
|:--|:----------------------|--------:|--------:|--------:|--------:|--------:|--------:|
|1  |weightedMedian         | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|2  |limma::weighted.median | 1.509551| 1.409938| 1.434577| 1.431985| 1.474038| 1.905769|
|3  |cwhmisc::w.median      | 2.096193| 1.931862| 1.898161| 1.916387| 1.906271| 1.651379|
|4  |laeken::weightedMedian | 2.944170| 2.747892| 2.820528| 2.768554| 2.761070| 6.394712|

_Figure: Benchmarking of weightedMedian(), limma::weighted.median(), cwhmisc::w.median() and laeken::weightedMedian() on n = 1000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/weightedMedian,n=1000,benchmark.png)

### n = 10000 vector

```r
> x <- data[["n = 10000"]]
> w <- runif(length(x))
> gc()
           used  (Mb) gc trigger  (Mb)  max used  (Mb)
Ncells  5397380 288.3    8529671 455.6   8529671 455.6
Vcells 10489485  80.1   39910282 304.5 101881463 777.3
> stats <- microbenchmark(weightedMedian = weightedMedian(x, w = w, ties = "mean", na.rm = FALSE), 
+     `limma::weighted.median` = limma_weighted.median(x, w = w, na.rm = FALSE), `cwhmisc::w.median` = cwhmisc_w.median(x, 
+         w = w), `laeken::weightedMedian` = laeken_weightedMedian(x, w = w), unit = "ms")
```

_Table: Benchmarking of weightedMedian(), limma::weighted.median(), cwhmisc::w.median() and laeken::weightedMedian() on n = 10000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr                   |      min|        lq|      mean|   median|        uq|      max|
|:--|:----------------------|--------:|---------:|---------:|--------:|---------:|--------:|
|2  |limma::weighted.median | 0.545187| 0.6093825| 0.6492610| 0.619089| 0.6740665| 0.978052|
|1  |weightedMedian         | 0.578573| 0.6433315| 0.6766489| 0.659578| 0.6857380| 0.992166|
|4  |laeken::weightedMedian | 0.664967| 0.7302895| 0.7902390| 0.750556| 0.8371090| 1.129962|
|3  |cwhmisc::w.median      | 0.699658| 0.7634875| 0.8327451| 0.785022| 0.8535205| 1.143068|


|   |expr                   |      min|       lq|     mean|   median|       uq|      max|
|:--|:----------------------|--------:|--------:|--------:|--------:|--------:|--------:|
|2  |limma::weighted.median | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.000000|
|1  |weightedMedian         | 1.061238| 1.055710| 1.042183| 1.065401| 1.017315| 1.014431|
|4  |laeken::weightedMedian | 1.219704| 1.198409| 1.217136| 1.212356| 1.241879| 1.155319|
|3  |cwhmisc::w.median      | 1.283336| 1.252887| 1.282605| 1.268028| 1.266226| 1.168719|

_Figure: Benchmarking of weightedMedian(), limma::weighted.median(), cwhmisc::w.median() and laeken::weightedMedian() on n = 10000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/weightedMedian,n=10000,benchmark.png)

### n = 100000 vector

```r
> x <- data[["n = 100000"]]
> w <- runif(length(x))
> gc()
           used  (Mb) gc trigger  (Mb)  max used  (Mb)
Ncells  5397461 288.3    8529671 455.6   8529671 455.6
Vcells 10580051  80.8   39910282 304.5 101881463 777.3
> stats <- microbenchmark(weightedMedian = weightedMedian(x, w = w, ties = "mean", na.rm = FALSE), 
+     `limma::weighted.median` = limma_weighted.median(x, w = w, na.rm = FALSE), `cwhmisc::w.median` = cwhmisc_w.median(x, 
+         w = w), `laeken::weightedMedian` = laeken_weightedMedian(x, w = w), unit = "ms")
```

_Table: Benchmarking of weightedMedian(), limma::weighted.median(), cwhmisc::w.median() and laeken::weightedMedian() on n = 100000 data. The top panel shows times in milliseconds and the bottom panel shows relative times._



|   |expr                   |      min|       lq|     mean|   median|       uq|       max|
|:--|:----------------------|--------:|--------:|--------:|--------:|--------:|---------:|
|2  |limma::weighted.median | 4.733150| 5.277121| 5.913677| 5.347941| 5.499855| 27.941903|
|4  |laeken::weightedMedian | 5.125208| 5.901288| 6.582535| 6.083902| 7.258841| 14.344677|
|3  |cwhmisc::w.median      | 6.130579| 6.908249| 7.574134| 7.038625| 7.916936| 13.601538|
|1  |weightedMedian         | 7.185838| 7.728294| 7.940226| 7.854243| 8.290318|  8.848144|


|   |expr                   |      min|       lq|     mean|   median|       uq|       max|
|:--|:----------------------|--------:|--------:|--------:|--------:|--------:|---------:|
|2  |limma::weighted.median | 1.000000| 1.000000| 1.000000| 1.000000| 1.000000| 1.0000000|
|4  |laeken::weightedMedian | 1.082832| 1.118278| 1.113104| 1.137616| 1.319824| 0.5133751|
|3  |cwhmisc::w.median      | 1.295243| 1.309094| 1.280782| 1.316137| 1.439481| 0.4867792|
|1  |weightedMedian         | 1.518194| 1.464491| 1.342689| 1.468648| 1.507370| 0.3166622|

_Figure: Benchmarking of weightedMedian(), limma::weighted.median(), cwhmisc::w.median() and laeken::weightedMedian() on n = 100000 data.  Outliers are displayed as crosses.  Times are in milliseconds._

![](figures/weightedMedian,n=100000,benchmark.png)


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
[13] RSQLite_2.2.8           lattice_0.20-44         limma_3.48.3           
[16] glue_1.4.2              digest_0.6.27           XVector_0.32.0         
[19] colorspace_2.0-2        Matrix_1.3-4            XML_3.99-0.7           
[22] pkgconfig_2.0.3         zlibbioc_1.38.0         genefilter_1.74.0      
[25] purrr_0.3.4             ergm_4.1.2              xtable_1.8-4           
[28] scales_1.1.1            tibble_3.1.4            annotate_1.70.0        
[31] KEGGREST_1.32.0         farver_2.1.0            generics_0.1.0         
[34] IRanges_2.26.0          ellipsis_0.3.2          cachem_1.0.6           
[37] withr_2.4.2             BiocGenerics_0.38.0     mime_0.11              
[40] survival_3.2-13         magrittr_2.0.1          crayon_1.4.1           
[43] statnet.common_4.5.0    memoise_2.0.0           laeken_0.5.1           
[46] fansi_0.5.0             R.cache_0.15.0          MASS_7.3-54            
[49] R.rsp_0.44.0            progressr_0.8.0         tools_4.1.1            
[52] lifecycle_1.0.0         S4Vectors_0.30.0        trust_0.1-8            
[55] munsell_0.5.0           tabby_0.0.1-9001        AnnotationDbi_1.54.1   
[58] Biostrings_2.60.2       compiler_4.1.1          GenomeInfoDb_1.28.1    
[61] rlang_0.4.11            grid_4.1.1              RCurl_1.98-1.4         
[64] cwhmisc_6.6             rappdirs_0.3.3          startup_0.15.0         
[67] labeling_0.4.2          bitops_1.0-7            base64enc_0.1-3        
[70] boot_1.3-28             gtable_0.3.0            DBI_1.1.1              
[73] markdown_1.1            R6_2.5.1                lpSolveAPI_5.5.2.0-17.7
[76] rle_0.9.2               dplyr_1.0.7             fastmap_1.1.0          
[79] bit_4.0.4               utf8_1.2.2              parallel_4.1.1         
[82] Rcpp_1.0.7              vctrs_0.3.8             png_0.1-7              
[85] DEoptimR_1.0-9          tidyselect_1.1.1        xfun_0.25              
[88] coda_0.19-4            
```
Total processing time was 7.65 secs.


### Reproducibility
To reproduce this report, do:
```r
html <- matrixStats:::benchmark('weightedMedian')
```

[RSP]: https://cran.r-project.org/package=R.rsp
[matrixStats]: https://cran.r-project.org/package=matrixStats

[StackOverflow:colMins?]: https://stackoverflow.com/questions/13676878 "Stack Overflow: fastest way to get Min from every column in a matrix?"
[StackOverflow:colSds?]: https://stackoverflow.com/questions/17549762 "Stack Overflow: Is there such 'colsd' in R?"
[StackOverflow:rowProds?]: https://stackoverflow.com/questions/20198801/ "Stack Overflow: Row product of matrix and column sum of matrix"

---------------------------------------
Copyright Henrik Bengtsson. Last updated on 2021-08-25 19:32:29 (+0200 UTC). Powered by [RSP].

<script>
 var link = document.createElement('link');
 link.rel = 'icon';
 link.href = "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAMAAABEpIrGAAAA21BMVEUAAAAAAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8BAf4CAv0DA/wdHeIeHuEfH+AgIN8hId4lJdomJtknJ9g+PsE/P8BAQL9yco10dIt1dYp3d4h4eIeVlWqWlmmXl2iYmGeZmWabm2Tn5xjo6Bfp6Rb39wj4+Af//wA2M9hbAAAASXRSTlMAAQIJCgsMJSYnKD4/QGRlZmhpamtsbautrrCxuru8y8zN5ebn6Pn6+///////////////////////////////////////////LsUNcQAAAS9JREFUOI29k21XgkAQhVcFytdSMqMETU26UVqGmpaiFbL//xc1cAhhwVNf6n5i5z67M2dmYOyfJZUqlVLhkKucG7cgmUZTybDz6g0iDeq51PUr37Ds2cy2/C9NeES5puDjxuUk1xnToZsg8pfA3avHQ3lLIi7iWRrkv/OYtkScxBIMgDee0ALoyxHQBJ68JLCjOtQIMIANF7QG9G9fNnHvisCHBVMKgSJgiz7nE+AoBKrAPA3MgepvgR9TSCasrCKH0eB1wBGBFdCO+nAGjMVGPcQb5bd6mQRegN6+1axOs9nGfYcCtfi4NQosdtH7dB+txFIpXQqN1p9B/asRHToyS0jRgpV7nk4nwcq1BJ+x3Gl/v7S9Wmpp/aGquum7w3ZDyrADFYrl8vHBH+ev9AUASW1dmU4h4wAAAABJRU5ErkJggg=="
 document.getElementsByTagName('head')[0].appendChild(link);
</script>



