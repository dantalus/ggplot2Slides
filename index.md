---
title       : Data visualization with ggplot2
subtitle    : Cork R-User's Group
author      : Darren L Dahly
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : ir_black     # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
--- 
<br>
<br>
<center>![](gg.png)</center>
<br>
<br>

<center>http://vita.had.co.nz/papers/layered-grammar.pdf</center>

--- 

## ggplot2 works with dataframes


```r
   require(ggplot2)
   head(iris)
```

```
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1          5.1         3.5          1.4         0.2  setosa
## 2          4.9         3.0          1.4         0.2  setosa
## 3          4.7         3.2          1.3         0.2  setosa
## 4          4.6         3.1          1.5         0.2  setosa
## 5          5.0         3.6          1.4         0.2  setosa
## 6          5.4         3.9          1.7         0.4  setosa
```

---

## Object class matters


```r
   lapply(iris, class)
```

```
## $Sepal.Length
## [1] "numeric"
## 
## $Sepal.Width
## [1] "numeric"
## 
## $Petal.Length
## [1] "numeric"
## 
## $Petal.Width
## [1] "numeric"
## 
## $Species
## [1] "factor"
```

---

## Minimal example



```r
   ggplot(iris, aes(x = Sepal.Width)) +
   geom_bar()  
```


---


<img src="assets/fig/unnamed-chunk-4-1.png" title="plot of chunk unnamed-chunk-4" alt="plot of chunk unnamed-chunk-4" style="display: block; margin: auto;" />

---


```r
   plot <- ggplot(iris, aes(x = Sepal.Width)) 
   plot <- plot + geom_bar()  
```

---


```r
   plot
```

<img src="assets/fig/unnamed-chunk-6-1.png" title="plot of chunk unnamed-chunk-6" alt="plot of chunk unnamed-chunk-6" style="display: block; margin: auto;" />

---

## Data


```r
   ggplot(iris[1:10, ], aes(x = Sepal.Width)) +
   geom_bar()  
```

<img src="assets/fig/unnamed-chunk-7-1.png" title="plot of chunk unnamed-chunk-7" alt="plot of chunk unnamed-chunk-7" style="display: block; margin: auto;" />

---


```r
   ggplot(subset(iris, Species == "setosa"), aes(x = Sepal.Width)) +
   geom_bar()  
```

<img src="assets/fig/unnamed-chunk-8-1.png" title="plot of chunk unnamed-chunk-8" alt="plot of chunk unnamed-chunk-8" style="display: block; margin: auto;" />

---


```r
   require(dplyr)
   
   iris %>%
   filter(Species == "virginica") %>%

   ggplot(aes(x = Sepal.Width)) +
   geom_bar()  
```

<img src="assets/fig/unnamed-chunk-9-1.png" title="plot of chunk unnamed-chunk-9" alt="plot of chunk unnamed-chunk-9" style="display: block; margin: auto;" />



