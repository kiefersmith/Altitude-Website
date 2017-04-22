---
author: realdataweb
comments: true
date: 2017-03-31 02:27:08+00:00
layout: post
link: https://realdataweb.wordpress.com/2017/03/31/take-your-data-frames-to-the-next-level/
slug: take-your-data-frames-to-the-next-level
title: Take your data frames to the next level.
wordpress_id: 457
tags:
- data
- data science
- Programming
- R
---









![leo](https://realdataweb.files.wordpress.com/2017/03/leo.jpg)

In R-rockstar Hadley Wickham’s book ([Free Book – R for Data Science](https://realdataweb.wordpress.com/2017/01/06/free-book-r-for-data-science/)), [the section on model building](http://r4ds.had.co.nz/model-building.html) elaborates on something pretty cool that I had no idea about - list columns.

Most of us have probably seen the following data frame column format:

    
    <code>df <- data.frame("col_uno" = c(1,2,3),"col_dos" = c('a','b','c'), "col_tres" = factor(c("google", "apple", "amazon")))</code>


And the output:

    
    <code>df</code>



    
    <code>##   col_uno col_dos col_tres
    ## 1       1       a   google
    ## 2       2       b    apple
    ## 3       3       c   amazon</code>


This is an awesome way to organize data and one of R’s strong points. However, we can use list functionality to go deeper. Check this out:

    
    <code>library(tidyverse)
    library(datasets)</code>



    
    <code>head(iris)</code>



    
    <code>##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ## 1          5.1         3.5          1.4         0.2  setosa
    ## 2          4.9         3.0          1.4         0.2  setosa
    ## 3          4.7         3.2          1.3         0.2  setosa
    ## 4          4.6         3.1          1.5         0.2  setosa
    ## 5          5.0         3.6          1.4         0.2  setosa
    ## 6          5.4         3.9          1.7         0.4  setosa</code>



    
    <code>nested <- iris %>%
     group_by(Species) %>%
     nest()
    </code>



    
    # A tibble: 3 × 2
     Species          data
     <fctr>          <list>
    1 setosa        <tibble [50 × 4]>
    2 versicolor    <tibble [50 × 4]>
    3 virginica     <tibble [50 × 4]>


Using `nest` we can compartmentalize our data frame for readability and more efficient iteration.  As a simple example, we can use `map` from the `purrr` package to compute the mean of each column in our nested data.

    
    <code>means <- map(nested$data, colMeans)</code>



    
    <code>## [[1]]
    ## Sepal.Length  Sepal.Width Petal.Length  Petal.Width 
    ##        5.006        3.428        1.462        0.246 
    ## 
    ## [[2]]
    ## Sepal.Length  Sepal.Width Petal.Length  Petal.Width 
    ##        5.936        2.770        4.260        1.326 
    ## 
    ## [[3]]
    ## Sepal.Length  Sepal.Width Petal.Length  Petal.Width 
    ##        6.588        2.974        5.552        2.026</code>


Once you’re done messing around with data-ception, use `unnest` to revert your data back to its original state.

    
    <code>head(unnest(nested))</code>



    
    <code>## # A tibble: 6 × 5
    ##   Species Sepal.Length Sepal.Width Petal.Length Petal.Width
    ##                                  
    ## 1  setosa          5.1         3.5          1.4         0.2
    ## 2  setosa          4.9         3.0          1.4         0.2
    ## 3  setosa          4.7         3.2          1.3         0.2
    ## 4  setosa          4.6         3.1          1.5         0.2
    ## 5  setosa          5.0         3.6          1.4         0.2
    ## 6  setosa          5.4         3.9          1.7         0.4</code>


I was pretty excited to learn about this property of data.frames and will definitely make use of it in the future. If you have any neat examples of nested dataset usage, please feel free to share in the comments.  As always, I'm happy to answer questions or talk data!

Kiefer Smith


