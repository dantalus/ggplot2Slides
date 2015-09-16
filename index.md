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

<br>
<br>
<center>![](ex1.png)</center>
<br>
<br>

---

<br>
<br>
<center>![](ex2.png)</center>
<br>
<br>

---

<br>
<br>
<center>![](ex3.png)</center>
<br>
<br>

---

<br>
<br>
<center>![](ex4.png)</center>
<br>
<br>

---

<br>
<br>
<center>![](ex5.png)</center>
<br>
<br>

---

<br>
<br>
<center>![](ex6.png)</center>
<br>
<br>

---

<br>
<br>
<center>![](ex7.png)</center>
<br>
<br>

---

<br>
<br>
<center>![](ex8.png)</center>
<br>
<br>

---

<br>
<br>
<center>![](ex9.png)</center>
<br>
<br>

---

<br>
<br>
<center>![](ex10.png)</center>
<br>
<br>

---

<br>
<br>
<center>![](ex11.png)</center>
<br>
<br>

---

<br>
<br>
<center>![](ex12.png)</center>
<br>
<br>

---

<br>
<br>
<center>![](ex13.png)</center>
<br>
<br>

---

<br>
<br>
<center>![](ex14.png)</center>
<br>
<br>

---

<br>
<br>
<center>![](ex15.png)</center>
<br>
<br>

---

<br>
<br>
<center>![](ex16.png)</center>
<br>
<br>

---

<br>
<br>
<center>![](ex17.png)</center>
<br>
<br>

---

## ggplot2 works with dataframes


```r
   library(ggplot2)
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


<img src="assets/fig/first plot-1.png" title="plot of chunk first plot" alt="plot of chunk first plot" style="display: block; margin: auto;" />

---


```r
   plot <- ggplot(iris, aes(x = Sepal.Width)) 
   plot <- plot + geom_bar()  
```

---


```r
   plot
```

<img src="assets/fig/as object 2-1.png" title="plot of chunk as object 2" alt="plot of chunk as object 2" style="display: block; margin: auto;" />

---

## Data


```r
   ggplot(iris[1:10, ], aes(x = Sepal.Width)) +
   geom_bar()  
```

<img src="assets/fig/index data-1.png" title="plot of chunk index data" alt="plot of chunk index data" style="display: block; margin: auto;" />

---


```r
   ggplot(subset(iris, Species == "setosa"), aes(x = Sepal.Width)) +
   geom_bar()  
```

<img src="assets/fig/subset data-1.png" title="plot of chunk subset data" alt="plot of chunk subset data" style="display: block; margin: auto;" />

---


```r
   library(dplyr)
   
   iris %>%
   filter(Species == "virginica") %>%

   ggplot(aes(x = Sepal.Width)) +
   geom_bar()  
```

<img src="assets/fig/pipe data-1.png" title="plot of chunk pipe data" alt="plot of chunk pipe data" style="display: block; margin: auto;" />

---

## Class matters


```r
  iris %>%
  mutate(Sepal.Width = factor(round(Sepal.Width, 0))) %>%
  
  ggplot(aes(x = Sepal.Width)) +
  geom_bar() 
```

<img src="assets/fig/factor bar chart-1.png" title="plot of chunk factor bar chart" alt="plot of chunk factor bar chart" style="display: block; margin: auto;" />

---



```r
  iris %>%
  mutate(Sepal.Width = round(Sepal.Width, 0)) %>%
  
  ggplot(aes(x = Sepal.Width)) +
  geom_bar() 
```

<img src="assets/fig/numeric bar chart-1.png" title="plot of chunk numeric bar chart" alt="plot of chunk numeric bar chart" style="display: block; margin: auto;" />

---

## aes - Aesthetic Mapping

### x-axis
### y-axis
### color/fill
### shape/linetype
### size
### alpha

---



```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length)) +
  geom_point() 
```

<img src="assets/fig/iris x y-1.png" title="plot of chunk iris x y" alt="plot of chunk iris x y" style="display: block; margin: auto;" />

---



```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length, color = Species)) +
  geom_point() 
```

<img src="assets/fig/iris color-1.png" title="plot of chunk iris color" alt="plot of chunk iris color" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length, size = Species)) +
  geom_point() 
```

<img src="assets/fig/iris size-1.png" title="plot of chunk iris size" alt="plot of chunk iris size" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length, shape = Species)) +
  geom_point() 
```

<img src="assets/fig/iris shape-1.png" title="plot of chunk iris shape" alt="plot of chunk iris shape" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length, 
                   shape = Species, color = Sepal.Length, size = Sepal.Width)) +
  geom_point() 
```

<img src="assets/fig/iris max-1.png" title="plot of chunk iris max" alt="plot of chunk iris max" style="display: block; margin: auto;" />

---


```r
  ggplot(mpg, aes(x = cty, y = hwy, shape = drv, color = class, size = cyl)) +
  geom_point() 
```

<img src="assets/fig/mpg max-1.png" title="plot of chunk mpg max" alt="plot of chunk mpg max" style="display: block; margin: auto;" />

