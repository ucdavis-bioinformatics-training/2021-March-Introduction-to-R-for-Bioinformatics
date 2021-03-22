---
title: "Challenge Solutions"
author: "UC Davis Bioinformatics Core"
date: "3/16/2021"
output:
  html_document:
    keep_md: TRUE
---



### mtcars


```r
# using only functions already seen
mtcars_avg <- colSums(mtcars) / nrow(mtcars)
mtcars2 <- rbind(mtcars, mtcars_avg)
rownames(mtcars2) <- c(rownames(mtcars), "avg")
mtcars2$hp.gt.100 <- mtcars2$hp > 100
mtcars2

# simplified
mtcars3 <- rbind(mtcars, "avg" = colMeans(mtcars))
mtcars3$hp.gt.100 <- mtcars3$hp > 100
mtcars3
```

### iris


```r
table(iris[iris$Sepal.Length > 6, "Species"])

# a data frame with two columns: species and sepal + petal
data.frame(Species = iris$Species,
           Length.Sum = iris$Sepal.Length + iris$Petal.Length)
```

### apply

```r
min_max_norm <- function(x) {
    (x-min(x))/(max(x)-min(x))
}

dnorm = t(apply(data2,MARGIN=1,min_max_norm))

l2fc <- function(x,y) {
    log2(x/y)
}

l2fc_all <- function(y) {
    apply(dnorm,MARGIN=2,function(x) l2fc(x,y))
}

for (samp in colnames(dnorm)) {
    print(l2fc_all(dnorm[,samp]))
}
```
