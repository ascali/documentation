---
title: geom_quantile in ggplot2 | Examples | Plotly
name: geom_quantile
permalink: ggplot2/geom_quantile/
description: How to use geom_quantile with Plotly.
layout: base
thumbnail: thumbnail/geom_quantile.jpg
language: ggplot2
page_type: example_index
has_thumbnail: true
display_as: statistical
order: 4
output:
  html_document:
    keep_md: true
---



### New to Plotly?

Plotly's R library is free and open source!<br>
[Get started](https://plot.ly/r/getting-started/) by downloading the client and [reading the primer](https://plot.ly/r/getting-started/).<br>
You can set up Plotly to work in [online](https://plot.ly/r/getting-started/#hosting-graphs-in-your-online-plotly-account) or [offline](https://plot.ly/r/offline/) mode.<br>
We also have a quick-reference [cheatsheet](https://images.plot.ly/plotly-documentation/images/r_cheat_sheet.pdf) (new!) to help you get started!

### Version Check

Version 4 of Plotly's R package is now [available](https://plot.ly/r/getting-started/#installation)!<br>
Check out [this post](http://moderndata.plot.ly/upgrading-to-plotly-4-0-and-above/) for more information on breaking changes and new features available in this version.


```r
library(plotly)
packageVersion('plotly')
```

```
## [1] '4.9.0.9000'
```

### Basic Example
While common linear regression is a method of estimating the conditional mean of variable y based on the values of variable(s) x, quantile regression is a method that can give the conditional median (50th percentile) as well as any other quantile.

[This dataset](https://stat.ethz.ch/R-manual/R-devel/library/MASS/html/birthwt.html) gives the effect of the mother's weight on her baby's birth weight, further divided according to whether the mother smokes or not. The line shows the *median* birth weight conditional on these two other variables.


```r
library(plotly)
library(MASS)

df <- MASS::birthwt

df <- with(df, { #Make sure variables properly show up as categories
  race <- factor(race, labels = c("white", "black", "other"))
  ptd <- factor(ptl > 0)
  ftv <- factor(ftv)
  levels(ftv)[-(1:2)] <- "2+"
  data.frame(low = factor(low), age, lwt, race, smoke = (smoke > 0),
             ptd, ht = (ht > 0), ui = (ui > 0), ftv, bwt)
})

p <- ggplot(df, aes(lwt, bwt, colour = smoke)) +
  geom_point(size = 1) +
  geom_quantile(quantiles = 0.5)

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = api_create(p, filename="geom_quantile/basic")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4422.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>


### With Quantiles
geom\_quantile is capable of showing more than just the conditional median: here we show the median, the 10th percentile, and 90th percentiles as well. We see that, among nonsmokers, the likelihood of underweight babies decreases significantly as the mother's weight increases, but that mothers of all weights are roughly equally likely to give birth to the heaviest babies. Conversely, among smoking mothers, the likelihood of underweight babies seem to *increase* as mother's weight increases. 

Given the small sample size for this dataset, it's wise not to draw too many conclusions; this is meant to illustrate the purpose of quantile regression. You can also adjust the lines' appearance.


```r
library(plotly)
library(MASS)
library(dplyr)

df <- MASS::birthwt

df <- with(df, {
  race <- factor(race, labels = c("white", "black", "other"))
  ptd <- factor(ptl > 0)
  ftv <- factor(ftv)
  levels(ftv)[-(1:2)] <- "2+"
  data.frame(low = factor(low), age, lwt, race, smoke = (smoke > 0),
             ptd, ht = (ht > 0), ui = (ui > 0), ftv, bwt)
})

p <- ggplot(df, aes(lwt, bwt, colour=smoke)) +
  geom_point(size = 1) +
  geom_quantile(quantiles = c(0.1, 0.5, 0.9), size = 2, aes(alpha = ..quantile..)) +
  scale_alpha(range = c(0.3, 0.7))
p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = api_create(p, filename="geom_quantile/quantiles")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/5876.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

Reference: [ggplot2 docs](http://ggplot2.tidyverse.org/reference/geom_quantile.html#examples)

### Reference

See [https://plot.ly/r/reference](https://plot.ly/r/reference) for more information and options!
