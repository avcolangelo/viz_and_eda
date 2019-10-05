ggplot 1
================
Alexis Colangelo
10/5/2019

## Create the weather data

``` r
weather_df = 
  rnoaa::meteo_pull_monitors(c("USW00094728", "USC00519397", "USS0023B17S"),
                      var = c("PRCP", "TMIN", "TMAX"),
                      date_min = "2017-01-01",
                      date_max = "2017-12-31") %>%
  mutate(
    name = recode(id, USW00094728 = "CentralPark_NY", 
                      USC00519397 = "Waikiki_HA",
                      USS0023B17S = "Waterhole_WA"),
    tmin = tmin / 10,
    tmax = tmax / 10) %>%
  select(name, id, everything())
```

    ## Registered S3 method overwritten by 'crul':
    ##   method                 from
    ##   as.character.form_file httr

    ## Registered S3 method overwritten by 'hoardr':
    ##   method           from
    ##   print.cache_info httr

    ## file path:          C:\Users\Lexi\AppData\Local\rnoaa\rnoaa\Cache/ghcnd/USW00094728.dly

    ## file last updated:  2019-09-09 16:19:32

    ## file min/max dates: 1869-01-01 / 2019-09-30

    ## file path:          C:\Users\Lexi\AppData\Local\rnoaa\rnoaa\Cache/ghcnd/USC00519397.dly

    ## file last updated:  2019-09-09 16:20:09

    ## file min/max dates: 1965-01-01 / 2019-09-30

    ## file path:          C:\Users\Lexi\AppData\Local\rnoaa\rnoaa\Cache/ghcnd/USS0023B17S.dly

    ## file last updated:  2019-09-09 16:20:22

    ## file min/max dates: 1999-09-01 / 2019-09-30

## Create a ggplot

``` r
ggplot(weather_df, aes(x = tmin, y = tmax)) + geom_point()
```

    ## Warning: Removed 15 rows containing missing values (geom_point).

![](viz_i_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

## Alternate way of making this plot

``` r
weather_df %>%
  ggplot(aes(x = tmin, y = tmax)) + geom_point()
```

    ## Warning: Removed 15 rows containing missing values (geom_point).

![](viz_i_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

saving initial plots

``` r
scatterplot = weather_df %>%
  ggplot(aes(x = tmin, y = tmax)) + geom_point()

scatterplot
```

    ## Warning: Removed 15 rows containing missing values (geom_point).

![](viz_i_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

adding color:

``` r
weather_df %>%
  ggplot(aes(x = tmin, y = tmax)) + geom_point(aes(color = name))
```

    ## Warning: Removed 15 rows containing missing values (geom_point).

![](viz_i_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

adding transparency:

``` r
weather_df %>%
  ggplot(aes(x = tmin, y = tmax)) + geom_point(aes(color = name), alpha = .4)
```

    ## Warning: Removed 15 rows containing missing values (geom_point).

![](viz_i_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

this

``` r
weather_df %>%
  ggplot(aes(x = tmin, y = tmax)) + geom_point(aes(color = name), alpha = .4) + geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'

    ## Warning: Removed 15 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 15 rows containing missing values (geom_point).

![](viz_i_files/figure-gfm/unnamed-chunk-6-1.png)<!-- --> vs.

``` r
weather_df %>%
  ggplot(aes(x = tmin, y = tmax, color = name)) + geom_point(alpha = .4) + geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

    ## Warning: Removed 15 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 15 rows containing missing values (geom_point).

![](viz_i_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->
