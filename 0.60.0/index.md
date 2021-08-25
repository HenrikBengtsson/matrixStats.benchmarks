



[matrixStats]: Benchmark report

---------------------------------------



# Benchmarks

List of benchmark report for some of the functions available in the [matrixStats] package.


* [allocMatrix()](allocMatrix.html)
* [allocVector()](allocVector.html)
* [anyMissing_subset()](anyMissing_subset.html)
* [anyMissing()](anyMissing.html)
* [binCounts_subset()](binCounts_subset.html)
* [binCounts()](binCounts.html)
* [binMeans_subset()](binMeans_subset.html)
* [binMeans()](binMeans.html)
* [colAlls_subset() and rowAlls_subset()](colRowAlls_subset.html)
* [colAlls() and rowAlls()](colRowAlls.html)
* [colAnyMissings_subset() and rowAnyMissings_subset()](colRowAnyMissings_subset.html)
* [colAnyMissings() and rowAnyMissings()](colRowAnyMissings.html)
* [colAnys_subset() and rowAnys_subset()](colRowAnys_subset.html)
* [colAnys() and rowAnys()](colRowAnys.html)
* [colCounts_subset() and rowCounts_subset()](colRowCounts_subset.html)
* [colCounts() and rowCounts()](colRowCounts.html)
* [colCummins_subset() and rowCummins_subset()](colRowCummins_subset.html)
* [colCummins() and rowCummins()](colRowCummins.html)
* [colCumprods_subset() and rowCumprods_subset()](colRowCumprods_subset.html)
* [colCumprods() and rowCumprods()](colRowCumprods.html)
* [colCumsums_subset() and rowCumsums_subset()](colRowCumsums_subset.html)
* [colCumsums() and rowCumsums()](colRowCumsums.html)
* [colDiffs_subset() and rowDiffs_subset()](colRowDiffs_subset.html)
* [colDiffs() and rowDiffs()](colRowDiffs.html)
* [colLogSumExps_subset() and rowLogSumExps_subset()](colRowLogSumExps_subset.html)
* [colLogSumExps() and rowLogSumExps()](colRowLogSumExps.html)
* [colMads_subset() and rowMads_subset()](colRowMads_subset.html)
* [colMads() and rowMads()](colRowMads.html)
* [colMeans2_subset() and rowMeans2_subset()](colRowMeans2_subset.html)
* [colMeans2() and rowMeans2()](colRowMeans2.html)
* [colMedians_subset() and rowMedians_subset()](colRowMedians_subset.html)
* [colMedians() and rowMedians()](colRowMedians.html)
* [colMins_subset() and rowMins_subset()](colRowMins_subset.html)
* [colMins() and rowMins()](colRowMins.html)
* [colOrderStats_subset() and rowOrderStats_subset()](colRowOrderStats_subset.html)
* [colOrderStats() and rowOrderStats()](colRowOrderStats.html)
* [colProds_subset() and rowProds_subset()](colRowProds_subset.html)
* [colProds() and rowProds()](colRowProds.html)
* [colQuantiles_subset() and rowQuantiles_subset()](colRowQuantiles_subset.html)
* [colQuantiles() and rowQuantiles()](colRowQuantiles.html)
* [colRanges_subset() and rowRanges_subset()](colRowRanges_subset.html)
* [colRanges() and rowRanges()](colRowRanges.html)
* [colRanks_subset() and rowRanks_subset()](colRowRanks_subset.html)
* [colRanks() and rowRanks()](colRowRanks.html)
* [colSums2_subset() and rowSums2_subset()](colRowSums2_subset.html)
* [colSums2() and rowSums2()](colRowSums2.html)
* [colTabulates_subset() and rowTabulates_subset()](colRowTabulates_subset.html)
* [colTabulates() and rowTabulates()](colRowTabulates.html)
* [colVars_subset() and rowVars_subset()](colRowVars_subset.html)
* [colVars() and rowVars()](colRowVars.html)
* [colWeightedMeans_subset() and rowWeightedMeans_subset()](colRowWeightedMeans_subset.html)
* [colWeightedMeans() and rowWeightedMeans()](colRowWeightedMeans.html)
* [colWeightedMedians_subset() and rowWeightedMedians_subset()](colRowWeightedMedians_subset.html)
* [colWeightedMedians() and rowWeightedMedians()](colRowWeightedMedians.html)
* [count_subset()](count_subset.html)
* [count()](count.html)
* [indexByRow()](indexByRow.html)
* [logSumExp_subset()](logSumExp_subset.html)
* [logSumExp()](logSumExp.html)
* [madDiff_subset()](madDiff_subset.html)
* [madDiff()](madDiff.html)
* [mean2_subset()](mean2_subset.html)
* [mean2()](mean2.html)
* [product_subset()](product_subset.html)
* [product()](product.html)
* [sum2_subset()](sum2_subset.html)
* [sum2()](sum2.html)
* [t_tx_OP_y_subset()](t_tx_OP_y_subset.html)
* [t_tx_OP_y()](t_tx_OP_y.html)
* [varDiff_subset()](varDiff_subset.html)
* [varDiff()](varDiff.html)
* [weightedMean_subset()](weightedMean_subset.html)
* [weightedMean()](weightedMean.html)
* [weightedMedian_subset()](weightedMedian_subset.html)
* [weightedMedian()](weightedMedian.html)
* [x_OP_y_subset()](x_OP_y_subset.html)
* [x_OP_y()](x_OP_y.html)


## Appendix
To reproduce this page and all of its reports, do:
```r
path <- system.file("benchmarking", package = "matrixStats")
R.rsp::rfile("index.md.rsp", path = path)
```
_Note: Each of the above reports takes up to several minutes to complete._


[RSP]: https://cran.r-project.org/package=R.rsp
[matrixStats]: https://cran.r-project.org/package=matrixStats

[StackOverflow:colMins?]: https://stackoverflow.com/questions/13676878 "Stack Overflow: fastest way to get Min from every column in a matrix?"
[StackOverflow:colSds?]: https://stackoverflow.com/questions/17549762 "Stack Overflow: Is there such 'colsd' in R?"
[StackOverflow:rowProds?]: https://stackoverflow.com/questions/20198801/ "Stack Overflow: Row product of matrix and column sum of matrix"

---------------------------------------
Copyright Henrik Bengtsson. Last updated on 2021-08-25 18:41:23 (+0200 UTC). Powered by [RSP].

<script>
 var link = document.createElement('link');
 link.rel = 'icon';
 link.href = "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAMAAABEpIrGAAAA21BMVEUAAAAAAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8AAP8BAf4CAv0DA/wdHeIeHuEfH+AgIN8hId4lJdomJtknJ9g+PsE/P8BAQL9yco10dIt1dYp3d4h4eIeVlWqWlmmXl2iYmGeZmWabm2Tn5xjo6Bfp6Rb39wj4+Af//wA2M9hbAAAASXRSTlMAAQIJCgsMJSYnKD4/QGRlZmhpamtsbautrrCxuru8y8zN5ebn6Pn6+///////////////////////////////////////////LsUNcQAAAS9JREFUOI29k21XgkAQhVcFytdSMqMETU26UVqGmpaiFbL//xc1cAhhwVNf6n5i5z67M2dmYOyfJZUqlVLhkKucG7cgmUZTybDz6g0iDeq51PUr37Ds2cy2/C9NeES5puDjxuUk1xnToZsg8pfA3avHQ3lLIi7iWRrkv/OYtkScxBIMgDee0ALoyxHQBJ68JLCjOtQIMIANF7QG9G9fNnHvisCHBVMKgSJgiz7nE+AoBKrAPA3MgepvgR9TSCasrCKH0eB1wBGBFdCO+nAGjMVGPcQb5bd6mQRegN6+1axOs9nGfYcCtfi4NQosdtH7dB+txFIpXQqN1p9B/asRHToyS0jRgpV7nk4nwcq1BJ+x3Gl/v7S9Wmpp/aGquum7w3ZDyrADFYrl8vHBH+ev9AUASW1dmU4h4wAAAABJRU5ErkJggg=="
 document.getElementsByTagName('head')[0].appendChild(link);
</script>

