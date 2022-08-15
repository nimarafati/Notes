**Installing clusterProfiler**
- Install rJava (https://zhiyzuo.github.io/installation-rJava/). 
- Install older version of rvcheck. 
```
packageurl <- "https://cran.r-project.org/src/contrib/Archive/rvcheck/rvcheck_0.1.8.tar.gz"
install.packages(packageurl, repos=NULL, type="source")
remove.packages("clusterProfiler")
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("clusterProfiler")
```
