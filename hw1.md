p8105\_hw1\_yg2762
================
Yang Gao
9/23/2021

# problem 1

## load function

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.4     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.3     ✓ stringr 1.4.0
    ## ✓ readr   2.0.1     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

## create data frame

a random sample of size 10 from a standard Normal distribution;

a logical vector indicating whether elements of the sample are greater
than 0;

a character vector of length 10;

a factor vector of length 10, with 3 different factor “levels”.

``` r
set.seed(1)
problem1_df=
  tibble( 
    norm_samp = rnorm(10),
    norm_samp_pos = norm_samp>0,
    vec_char = c("1","2","3","4","5","6","7","8","9","10"),
    vec_factor = factor(c("1","2","3","2","1","3","1","3","2","1"))
  )
problem1_df
```

    ## # A tibble: 10 × 4
    ##    norm_samp norm_samp_pos vec_char vec_factor
    ##        <dbl> <lgl>         <chr>    <fct>     
    ##  1    -0.626 FALSE         1        1         
    ##  2     0.184 TRUE          2        2         
    ##  3    -0.836 FALSE         3        3         
    ##  4     1.60  TRUE          4        2         
    ##  5     0.330 TRUE          5        1         
    ##  6    -0.820 FALSE         6        3         
    ##  7     0.487 TRUE          7        1         
    ##  8     0.738 TRUE          8        3         
    ##  9     0.576 TRUE          9        2         
    ## 10    -0.305 FALSE         10       1

## take the mean value

``` r
mean_samp = mean(pull(problem1_df, norm_samp))
mean_samp
```

    ## [1] 0.1322028

``` r
mean_pos = mean(pull(problem1_df, norm_samp_pos))
mean_pos
```

    ## [1] 0.6

``` r
mean_vec_char = mean(pull(problem1_df, vec_char))
```

    ## Warning in mean.default(pull(problem1_df, vec_char)): argument is not numeric or
    ## logical: returning NA

``` r
mean_vec_factor = mean(pull(problem1_df,vec_factor))
```

    ## Warning in mean.default(pull(problem1_df, vec_factor)): argument is not numeric
    ## or logical: returning NA

The mean of variable norm\_samp is 0.132, the mean of norm\_samp\_pos is
0.6. The mean of character vector and factor vector cannot be calculated
because these two variables are not numeric or logical. (see Warning
message in the output).

### use code “as numeric”

``` r
pull(problem1_df,norm_samp_pos)
pos_num = as.numeric(problem1_df$norm_samp_pos)
mean(pos_num)

pull(problem1_df,vec_char)
vec_char_num = s.numeric(problem1_df$vec_char)
mean(vec_char_num)
                   
pull(problem1_df,vec_factor)
vec_factor_num = as.numeric(problem1_df$vec_factor)
mean(vec_factor_num)
```

`as.numeric` function converts elements in vectors into numeric version,
so we can calculate the mean. R treats FALSE=0 and TRUE=1 for logical
vectors.

# Problem 2

## load dataset

This is dataframe `penguins` contains 344 items and 8 variables.The data
contains `ncol("penguins")` columns and `nrow(penguins)` rows. The mean
flipper\_length is `mean(penguins$"flipper_length_mm",na.rm=TRUE)`.

    ## # A tibble: 344 × 8
    ##    species island    bill_length_mm bill_depth_mm flipper_length_mm body_mass_g
    ##    <fct>   <fct>              <dbl>         <dbl>             <int>       <int>
    ##  1 Adelie  Torgersen           39.1          18.7               181        3750
    ##  2 Adelie  Torgersen           39.5          17.4               186        3800
    ##  3 Adelie  Torgersen           40.3          18                 195        3250
    ##  4 Adelie  Torgersen           NA            NA                  NA          NA
    ##  5 Adelie  Torgersen           36.7          19.3               193        3450
    ##  6 Adelie  Torgersen           39.3          20.6               190        3650
    ##  7 Adelie  Torgersen           38.9          17.8               181        3625
    ##  8 Adelie  Torgersen           39.2          19.6               195        4675
    ##  9 Adelie  Torgersen           34.1          18.1               193        3475
    ## 10 Adelie  Torgersen           42            20.2               190        4250
    ## # … with 334 more rows, and 2 more variables: sex <fct>, year <int>

    ## [1] 8

    ## [1] 344

    ## [1] 200.9152

## making plot

``` r
ggplot(penguins,aes(x = bill_length_mm, y = flipper_length_mm,color=species)) + geom_point()
```

![](hw1_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
ggsave("scatter_plot.pdf", height = 4, width = 6)
```
