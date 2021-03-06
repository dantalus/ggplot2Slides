---
title       : Data visualization with ggplot2
subtitle    : Cork R-User's Group - September 16th, 2015
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

## ggplot2 works with data frames


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

### faceting

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

<img src="assets/fig/unnamed-chunk-1-1.png" title="plot of chunk unnamed-chunk-1" alt="plot of chunk unnamed-chunk-1" style="display: block; margin: auto;" />

---


```r
  ggplot(mpg, aes(x = cty, y = hwy, shape = drv, color = class)) +
  geom_point() +
  facet_wrap(~cyl)
```

<img src="assets/fig/unnamed-chunk-2-1.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" style="display: block; margin: auto;" />

---

## Layers


```r
  ggplot(mpg, aes(x = cty, y = hwy, color = cyl)) +
  geom_point() 
```

<img src="assets/fig/unnamed-chunk-3-1.png" title="plot of chunk unnamed-chunk-3" alt="plot of chunk unnamed-chunk-3" style="display: block; margin: auto;" />

---



```r
  ggplot(mpg, aes(x = cty, y = hwy, color = cyl)) +
  geom_point(color = "red") 
```

<img src="assets/fig/unnamed-chunk-4-1.png" title="plot of chunk unnamed-chunk-4" alt="plot of chunk unnamed-chunk-4" style="display: block; margin: auto;" />

---


```r
  ggplot(mpg, aes(x = cty, y = hwy)) +
  geom_point(aes(color = cyl)) 
```

<img src="assets/fig/unnamed-chunk-5-1.png" title="plot of chunk unnamed-chunk-5" alt="plot of chunk unnamed-chunk-5" style="display: block; margin: auto;" />

---


```r
  ggplot(mpg, aes(x = cty, y = hwy, color = cyl)) +
  geom_point() +
  geom_point(data = mpg[1:10, ], color = "red") 
```

<img src="assets/fig/unnamed-chunk-6-1.png" title="plot of chunk unnamed-chunk-6" alt="plot of chunk unnamed-chunk-6" style="display: block; margin: auto;" />

---

## Geometries

<br>
<br>

<center>http://docs.ggplot2.org/current/</center>

---

## Scatter plots

---


```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length)) +
  geom_point() 
```

<img src="assets/fig/unnamed-chunk-7-1.png" title="plot of chunk unnamed-chunk-7" alt="plot of chunk unnamed-chunk-7" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length)) +
  geom_jitter() 
```

<img src="assets/fig/unnamed-chunk-8-1.png" title="plot of chunk unnamed-chunk-8" alt="plot of chunk unnamed-chunk-8" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length)) +
  geom_jitter(size = 3.5, alpha = 0.5) 
```

<img src="assets/fig/unnamed-chunk-9-1.png" title="plot of chunk unnamed-chunk-9" alt="plot of chunk unnamed-chunk-9" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length, color = Species)) +
  geom_jitter(size = 3.5, alpha = 0.5) 
```

<img src="assets/fig/unnamed-chunk-10-1.png" title="plot of chunk unnamed-chunk-10" alt="plot of chunk unnamed-chunk-10" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length, color = Species)) +
  geom_jitter(size = 3.5, alpha = 0.5) +
  geom_smooth(method = "lm", se = FALSE)
```

<img src="assets/fig/unnamed-chunk-11-1.png" title="plot of chunk unnamed-chunk-11" alt="plot of chunk unnamed-chunk-11" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length, color = Species)) +
  geom_jitter(size = 3.5, alpha = 0.5) +
  geom_smooth(method = "lm", se = FALSE, color = "black")
```

<img src="assets/fig/unnamed-chunk-12-1.png" title="plot of chunk unnamed-chunk-12" alt="plot of chunk unnamed-chunk-12" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length, color = Species)) +
  geom_jitter(size = 3.5, alpha = 0.5) +
  geom_smooth(method = "lm", se = FALSE) +
  geom_smooth(method = "lm", se = FALSE, color = "black") 
```

<img src="assets/fig/unnamed-chunk-13-1.png" title="plot of chunk unnamed-chunk-13" alt="plot of chunk unnamed-chunk-13" style="display: block; margin: auto;" />

---


```r
  ggplot(mpg, aes(x = drv, y = class)) +
  geom_jitter(alpha = 0.5, position = position_jitter(width = 0.2, 
                                                      height = 0.2)) 
```

<img src="assets/fig/unnamed-chunk-14-1.png" title="plot of chunk unnamed-chunk-14" alt="plot of chunk unnamed-chunk-14" style="display: block; margin: auto;" />

---


```r
  ggplot(mpg, aes(x = drv, y = class, color = year)) +
  geom_jitter(position = position_jitter(width = 0.2, height = 0.2)) 
```

<img src="assets/fig/unnamed-chunk-15-1.png" title="plot of chunk unnamed-chunk-15" alt="plot of chunk unnamed-chunk-15" style="display: block; margin: auto;" />

---


```r
  ggplot(mpg, aes(x = drv, y = class, color = factor(year))) +
  geom_jitter(position = position_jitter(width = 0.2, height = 0.2)) 
```

<img src="assets/fig/unnamed-chunk-16-1.png" title="plot of chunk unnamed-chunk-16" alt="plot of chunk unnamed-chunk-16" style="display: block; margin: auto;" />

---

## Boxplots

---


```r
  ggplot(iris, aes(x = Species, y = Sepal.Length)) +
  geom_boxplot() 
```

<img src="assets/fig/unnamed-chunk-17-1.png" title="plot of chunk unnamed-chunk-17" alt="plot of chunk unnamed-chunk-17" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Species, y = Sepal.Length)) +
  geom_jitter() +
  geom_boxplot() 
```

<img src="assets/fig/unnamed-chunk-18-1.png" title="plot of chunk unnamed-chunk-18" alt="plot of chunk unnamed-chunk-18" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Species, y = Sepal.Length)) +
  geom_jitter(position = position_jitter(width = 0.2, height = 0.1)) +
  geom_boxplot(alpha = 0.5) 
```

<img src="assets/fig/unnamed-chunk-19-1.png" title="plot of chunk unnamed-chunk-19" alt="plot of chunk unnamed-chunk-19" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Species, y = Sepal.Length, color = Species)) +
  geom_jitter(position = position_jitter(width = 0.2, height = 0.1), 
              outlier.shape = NA) +
  geom_boxplot(alpha = 0.5) 
```

<img src="assets/fig/unnamed-chunk-20-1.png" title="plot of chunk unnamed-chunk-20" alt="plot of chunk unnamed-chunk-20" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Species, y = Sepal.Length, color = Species, 
                   fill = Species)) +
  geom_jitter(position = position_jitter(width = 0.2, height = 0.1)) +
  geom_boxplot(alpha = 0.5, outlier.shape = NA) 
```

<img src="assets/fig/unnamed-chunk-21-1.png" title="plot of chunk unnamed-chunk-21" alt="plot of chunk unnamed-chunk-21" style="display: block; margin: auto;" />

---



```r
  ggplot(iris, aes(x = Species, y = Sepal.Length, color = Species, 
                   fill = Species)) +
  geom_violin(alpha = 0.5) 
```

<img src="assets/fig/unnamed-chunk-22-1.png" title="plot of chunk unnamed-chunk-22" alt="plot of chunk unnamed-chunk-22" style="display: block; margin: auto;" />

---

## Line plots

---


```r
  ggplot(economics, aes(x = date, y = pop)) +
  geom_line() 
```

<img src="assets/fig/unnamed-chunk-23-1.png" title="plot of chunk unnamed-chunk-23" alt="plot of chunk unnamed-chunk-23" style="display: block; margin: auto;" />

---


```r
  ggplot(Orange, aes(x = age, y = circumference)) +
  geom_line()
```

<img src="assets/fig/unnamed-chunk-24-1.png" title="plot of chunk unnamed-chunk-24" alt="plot of chunk unnamed-chunk-24" style="display: block; margin: auto;" />

---


```r
  ggplot(Orange, aes(x = age, y = circumference, group = Tree)) +
  geom_line()
```

<img src="assets/fig/unnamed-chunk-25-1.png" title="plot of chunk unnamed-chunk-25" alt="plot of chunk unnamed-chunk-25" style="display: block; margin: auto;" />

---


```r
  ggplot(Orange, aes(x = age, y = circumference, group = Tree, color = Tree)) +
  geom_line()
```

<img src="assets/fig/unnamed-chunk-26-1.png" title="plot of chunk unnamed-chunk-26" alt="plot of chunk unnamed-chunk-26" style="display: block; margin: auto;" />

---


```r
  ggplot(Orange, aes(x = age, y = circumference, group = Tree, 
                     linetype = Tree, color = Tree)) +
  geom_line()
```

<img src="assets/fig/unnamed-chunk-27-1.png" title="plot of chunk unnamed-chunk-27" alt="plot of chunk unnamed-chunk-27" style="display: block; margin: auto;" />

---


```r
  ggplot(Orange, aes(x = age, y = circumference, group = Tree, 
                     linetype = Tree, color = Tree)) +
  geom_point() +
  geom_smooth(method = "lm", se = FALSE)
```

<img src="assets/fig/unnamed-chunk-28-1.png" title="plot of chunk unnamed-chunk-28" alt="plot of chunk unnamed-chunk-28" style="display: block; margin: auto;" />

---


```r
  ggplot(Orange, aes(x = age, y = circumference, group = Tree, 
                     linetype = Tree, color = Tree)) +
  geom_point() +
  geom_smooth(se = FALSE)
```

<img src="assets/fig/unnamed-chunk-29-1.png" title="plot of chunk unnamed-chunk-29" alt="plot of chunk unnamed-chunk-29" style="display: block; margin: auto;" />

---

## Bar plots

---


```r
  ggplot(mpg, aes(x = factor(cyl))) +
  geom_bar()
```

<img src="assets/fig/unnamed-chunk-30-1.png" title="plot of chunk unnamed-chunk-30" alt="plot of chunk unnamed-chunk-30" style="display: block; margin: auto;" />

---


```r
  ggplot(mpg, aes(x = factor(cyl))) +
  geom_bar() +
  coord_flip()
```

<img src="assets/fig/unnamed-chunk-31-1.png" title="plot of chunk unnamed-chunk-31" alt="plot of chunk unnamed-chunk-31" style="display: block; margin: auto;" />

---


```r
  mpg %>%
  group_by(cyl) %>%
  summarize(total = n()) %>%
  mutate(cyl = factor(cyl)) %>%
  mutate(cyl = reorder(cyl, total, max)) 
```

```
## Source: local data frame [4 x 2]
## 
##   cyl total
## 1   4    81
## 2   5     4
## 3   6    79
## 4   8    70
```

---


```r
  mpg %>%
  group_by(cyl) %>%
  summarize(total = n()) %>%
  mutate(cyl = factor(cyl)) %>%
  mutate(cyl = reorder(cyl, total, max)) %>%
  
  ggplot(aes(x = cyl, y = total)) +
  geom_bar(stat = "identity") +
  coord_flip()
```

<img src="assets/fig/unnamed-chunk-33-1.png" title="plot of chunk unnamed-chunk-33" alt="plot of chunk unnamed-chunk-33" style="display: block; margin: auto;" />

---


```r
  ggplot(mpg, aes(x = interaction(factor(cyl), class))) +
  geom_bar() +
  coord_flip()
```

<img src="assets/fig/unnamed-chunk-34-1.png" title="plot of chunk unnamed-chunk-34" alt="plot of chunk unnamed-chunk-34" style="display: block; margin: auto;" />

---


```r
  ggplot(mpg, aes(x = factor(cyl), fill = class)) +
  geom_bar()
```

<img src="assets/fig/unnamed-chunk-35-1.png" title="plot of chunk unnamed-chunk-35" alt="plot of chunk unnamed-chunk-35" style="display: block; margin: auto;" />

---


```r
  ggplot(mpg, aes(x = factor(cyl), fill = class)) +
  geom_bar(position = "dodge")
```

<img src="assets/fig/unnamed-chunk-36-1.png" title="plot of chunk unnamed-chunk-36" alt="plot of chunk unnamed-chunk-36" style="display: block; margin: auto;" />

---


```r
  mpg %>%
  group_by(cyl, class) %>%   
  summarize(subtotal = n()) %>%
  mutate(total = max(cumsum(subtotal))) %>%
  mutate(prop = subtotal/total) %>%
  head()
```

```
## Source: local data frame [6 x 5]
## Groups: cyl
## 
##   cyl      class subtotal total       prop
## 1   4    compact       32    81 0.39506173
## 2   4    midsize       16    81 0.19753086
## 3   4    minivan        1    81 0.01234568
## 4   4     pickup        3    81 0.03703704
## 5   4 subcompact       21    81 0.25925926
## 6   4        suv        8    81 0.09876543
```

---


```r
  mpg %>%
  group_by(cyl, class) %>%   
  summarize(subtotal = n()) %>%
  mutate(total = max(cumsum(subtotal))) %>%
  mutate(prop = subtotal/total) %>%  
  
  ggplot(aes(x = factor(cyl), fill = class, y = prop)) +
  geom_bar(position = "stack", stat = "identity")
```

<img src="assets/fig/unnamed-chunk-38-1.png" title="plot of chunk unnamed-chunk-38" alt="plot of chunk unnamed-chunk-38" style="display: block; margin: auto;" />

---


```r
  ggplot(mpg, aes(x = factor(cyl), y = cty)) +
  geom_bar(stat = "identity")
```

<img src="assets/fig/unnamed-chunk-39-1.png" title="plot of chunk unnamed-chunk-39" alt="plot of chunk unnamed-chunk-39" style="display: block; margin: auto;" />

---


```r
  mpg %>%
  group_by(cyl) %>%
  summarize(meancty = mean(cty)) 
```

```
## Source: local data frame [4 x 2]
## 
##   cyl  meancty
## 1   4 21.01235
## 2   5 20.50000
## 3   6 16.21519
## 4   8 12.57143
```

---


```r
  mpg %>%
  group_by(cyl) %>%
  summarize(meancty = mean(cty)) %>%
   
  ggplot(aes(x = factor(cyl), y = meancty)) +
  geom_bar(stat = "identity")
```

<img src="assets/fig/unnamed-chunk-41-1.png" title="plot of chunk unnamed-chunk-41" alt="plot of chunk unnamed-chunk-41" style="display: block; margin: auto;" />

---

## Heat maps

---


```r
  data_frame("ID" = c(1:50), 
             "A"  = sample(c(1:5), 50, replace = T),
             "B"  = sample(c(1:5), 50, replace = T),
             "C"  = sample(c(1:5), 50, replace = T),
             "D"  = sample(c(1:5), 50, replace = T),
             "E"  = sample(c(1:5), 50, replace = T),
             "G"  = sample(c(1:5), 50, replace = T)) %>% head()
```

```
## Source: local data frame [6 x 7]
## 
##   ID A B C D E G
## 1  1 3 2 1 1 3 4
## 2  2 5 4 1 4 2 3
## 3  3 5 3 3 3 2 3
## 4  4 2 4 3 1 1 2
## 5  5 4 4 1 5 1 5
## 6  6 4 1 3 1 2 3
```

---


```r
  library(tidyr) 
   
  data_frame("ID" = c(1:50), 
             "A"  = sample(c(1:5), 50, replace = T),
             "B"  = sample(c(1:5), 50, replace = T),
             "C"  = sample(c(1:5), 50, replace = T),
             "D"  = sample(c(1:5), 50, replace = T),
             "E"  = sample(c(1:5), 50, replace = T),
             "G"  = sample(c(1:5), 50, replace = T)) %>% 
  gather(question, value, A:G)  %>% 
  head()
```

```
## Source: local data frame [6 x 3]
## 
##   ID question value
## 1  1        A     1
## 2  2        A     1
## 3  3        A     1
## 4  4        A     5
## 5  5        A     3
## 6  6        A     4
```

---


```r
  data_frame("ID" = c(1:50), 
             "A"  = sample(c(1:5), 50, replace = T),
             "B"  = sample(c(1:5), 50, replace = T),
             "C"  = sample(c(1:5), 50, replace = T),
             "D"  = sample(c(1:5), 50, replace = T),
             "E"  = sample(c(1:5), 50, replace = T),
             "G"  = sample(c(1:5), 50, replace = T)) %>% 
  gather(question, value, A:G) %>%
  mutate(value = factor(value, 
                        labels = c("Weekly", 
                                    "Monthly/Quarterly", 
                                    "Yearly",
                                    "Not yet", 
                                    "Not my job")))  %>%
  head()
```

```
## Source: local data frame [6 x 3]
## 
##   ID question             value
## 1  1        A            Yearly
## 2  2        A        Not my job
## 3  3        A            Yearly
## 4  4        A Monthly/Quarterly
## 5  5        A            Yearly
## 6  6        A        Not my job
```

---



<img src="assets/fig/unnamed-chunk-46-1.png" title="plot of chunk unnamed-chunk-46" alt="plot of chunk unnamed-chunk-46" style="display: block; margin: auto;" />

---

## Scales

---


```r
  library(RColorBrewer) 
   
  ggplot(mpg, aes(x = factor(cyl), fill = class)) +
  geom_bar() +
  scale_fill_brewer(palette = "Set1")
```

<img src="assets/fig/unnamed-chunk-47-1.png" title="plot of chunk unnamed-chunk-47" alt="plot of chunk unnamed-chunk-47" style="display: block; margin: auto;" />

---


```r
  library(RColorBrewer) 
   
  ggplot(mpg, aes(x = factor(cyl), fill = class)) +
  geom_bar() +
  scale_fill_brewer(palette = "Blues")
```

<img src="assets/fig/unnamed-chunk-48-1.png" title="plot of chunk unnamed-chunk-48" alt="plot of chunk unnamed-chunk-48" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length, color = Species)) +
  geom_point() +
  scale_color_brewer(palette = "Set1")
```

<img src="assets/fig/unnamed-chunk-49-1.png" title="plot of chunk unnamed-chunk-49" alt="plot of chunk unnamed-chunk-49" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length, color = Species)) +
  geom_point() +
  scale_color_brewer(palette = "Reds")
```

<img src="assets/fig/unnamed-chunk-50-1.png" title="plot of chunk unnamed-chunk-50" alt="plot of chunk unnamed-chunk-50" style="display: block; margin: auto;" />

---


```r
 brewer.pal(6, "Reds")
```

```
## [1] "#FEE5D9" "#FCBBA1" "#FC9272" "#FB6A4A" "#DE2D26" "#A50F15"
```

```r
 brewer.pal(6, "Reds")[4:6]
```

```
## [1] "#FB6A4A" "#DE2D26" "#A50F15"
```

---


```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length, color = Species)) +
  geom_point() +
  scale_color_manual(values = brewer.pal(6, "Reds")[4:6])
```

<img src="assets/fig/unnamed-chunk-52-1.png" title="plot of chunk unnamed-chunk-52" alt="plot of chunk unnamed-chunk-52" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length, color = Species)) +
  geom_point() +
  scale_color_manual(guide = FALSE, values = brewer.pal(6, "Reds")[4:6])
```

<img src="assets/fig/unnamed-chunk-53-1.png" title="plot of chunk unnamed-chunk-53" alt="plot of chunk unnamed-chunk-53" style="display: block; margin: auto;" />

---

## ColorBrewer

<br>
<br>
<center>http://colorbrewer2.org/</center>

---


```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length, color = Species)) +
  geom_point() +
  scale_x_continuous(breaks = c(2, 3, 4, 5))
```

<img src="assets/fig/unnamed-chunk-54-1.png" title="plot of chunk unnamed-chunk-54" alt="plot of chunk unnamed-chunk-54" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length, color = Species)) +
  geom_point() +
  scale_x_continuous(limit = c(3, 4))
```

<img src="assets/fig/unnamed-chunk-55-1.png" title="plot of chunk unnamed-chunk-55" alt="plot of chunk unnamed-chunk-55" style="display: block; margin: auto;" />

---


```r
  ggplot(iris, aes(x = Sepal.Width, y = Sepal.Length, color = Species)) +
  geom_point() +
  scale_x_reverse()
```

<img src="assets/fig/unnamed-chunk-56-1.png" title="plot of chunk unnamed-chunk-56" alt="plot of chunk unnamed-chunk-56" style="display: block; margin: auto;" />

---


```r
  ggplot(mpg, aes(x = factor(cyl), fill = class)) +
  geom_bar() +
  scale_x_discrete(limits = c("4", "6", "8"))
```

<img src="assets/fig/unnamed-chunk-57-1.png" title="plot of chunk unnamed-chunk-57" alt="plot of chunk unnamed-chunk-57" style="display: block; margin: auto;" />

---

## Labels

---


```r
  ggplot(mpg, aes(x = factor(cyl), fill = class)) +
  geom_bar() +
  scale_x_discrete(limits = c("4", "6", "8")) +
  ggtitle("Title") +
  ylab("Number of observations") +
  xlab("Number of cylinders")
```

<img src="assets/fig/unnamed-chunk-58-1.png" title="plot of chunk unnamed-chunk-58" alt="plot of chunk unnamed-chunk-58" style="display: block; margin: auto;" />

---

## Themes


```r
  ggplot(mpg, aes(x = factor(cyl), fill = class)) +
  geom_bar() +
  scale_x_discrete(limits = c("4", "6", "8")) +
  ggtitle("Title") +
  ylab("Number of observations") +
  xlab("Number of cylinders") +
  theme_bw()
```

<img src="assets/fig/unnamed-chunk-59-1.png" title="plot of chunk unnamed-chunk-59" alt="plot of chunk unnamed-chunk-59" style="display: block; margin: auto;" />

---


```r
  ggplot(mpg, aes(x = factor(cyl), fill = class)) +
  geom_bar() +
  scale_x_discrete(limits = c("4", "6", "8")) +
  ggtitle("Title") +
  ylab("Number of observations") +
  xlab("Number of cylinders") +
  theme_bw() +
  theme(panel.grid = element_blank(),
  			panel.border = element_blank(),
  			axis.text.x = element_text(angle = 45, hjust = 1))
```

<img src="assets/fig/unnamed-chunk-60-1.png" title="plot of chunk unnamed-chunk-60" alt="plot of chunk unnamed-chunk-60" style="display: block; margin: auto;" />

---


```r
  ggplot(data, aes(x = question, y = as.factor(ID))) + 
  geom_tile(aes(fill = value)) +
  ylab("Each row is a person (n = 500)") +
  xlab("Survey Question") +
  scale_y_discrete(labels = "") +
  theme_bw() + 
  theme(text = element_text (color = "black", family = "serif"), 
        strip.background = element_blank(),
        panel.border = element_blank(), 
        panel.grid = element_blank(),
        axis.text.x = element_text (angle = 90), 
        axis.ticks.y = element_blank()) +
  scale_fill_brewer("", palette = "RdBu")
```

---

<img src="assets/fig/unnamed-chunk-62-1.png" title="plot of chunk unnamed-chunk-62" alt="plot of chunk unnamed-chunk-62" style="display: block; margin: auto;" />

---

## Themes

<br>
<br>
<center>http://docs.ggplot2.org/current/theme.html</center>

---

## Summary

- Data
- Map variables to visual properties (aesthetics)
- Choose useful geometries
- Take advantage of layers
- Modify scales as needed
- Add labels
- Customize your theme


