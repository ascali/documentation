---
title: ggplot2 facet_grid | Examples | Plotly
name: facet_grid
permalink: ggplot2/facet_grid/
redirect_from: ggplot2/facet/
description: How to make subplots with facet_wrap and facet_grid in ggplot2 and R.
layout: base
thumbnail: thumbnail/facet_grid.jpg
language: ggplot2
page_type: example_index
has_thumbnail: true
display_as: layout_opt
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
## [1] '4.5.6.9000'
```

### Basic


```r
library(reshape2)
library(plotly)

p <- ggplot(tips, aes(x=total_bill, y=tip/total_bill)) + geom_point(shape=1)

# Divide by levels of "sex", in the vertical direction
p <- p + facet_grid(sex ~ .)

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="facetgrid/basic")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4229.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Horizontal Grid


```r
library(reshape2)
library(plotly)

p <- ggplot(tips, aes(x=total_bill, y=tip/total_bill)) + geom_point(shape=1)

# Divide by levels of "sex", in the horizontal direction
p <- p + facet_grid(. ~ sex)

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="facetgrid/horizontal")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4231.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Free Scale


```r
library(reshape2)
library(plotly)

p <- ggplot(tips, aes(x=total_bill)) + geom_histogram(binwidth=2,colour="white")

# Histogram of total_bill, divided by sex and smoker
p <- p + facet_grid(sex ~ smoker)

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="facetgrid/free-scale")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4233.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Free Y Axis


```r
library(reshape2)
library(plotly)

p <- ggplot(tips, aes(x=total_bill)) + geom_histogram(binwidth=2,colour="white")

# Same as above, with scales="free_y"
p <- p + facet_grid(sex ~ smoker, scales="free_y")

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="facetgrid/y")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4235.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Varied Range


```r
library(reshape2)
library(plotly)

p <- ggplot(tips, aes(x=total_bill)) + geom_histogram(binwidth=2,colour="white")

# With panels that have the same scaling, but different range (and therefore different physical sizes)
p <- p + facet_grid(sex ~ smoker, scales="free", space="free")

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="facetgrid/range")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4237.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Time Series Data


```r
library(plotly)
require(scales)
require(gridExtra)

mymelt <- structure(list(mydate = structure(c(15340, 15340, 15340, 15340, 15340, 15340, 15340, 15340, 15340, 15340, 15340, 15340, 15371, 15371, 15371, 15371, 15371, 15371, 15371, 15371, 15371, 15371, 15371, 15371, 15400, 15400, 15400, 15400, 15400, 15400, 15400, 15400, 15400, 15400, 15400, 15400, 15431, 15431, 15431, 15431, 15431, 15431, 15431, 15431, 15431, 15431, 15431, 15431, 15461, 15461, 15461, 15461, 15461, 15461, 15461, 15461, 15461, 15461, 15461, 15461, 15492, 15492, 15492, 15492, 15492, 15492, 15492, 15492, 15492, 15492, 15492, 15492, 15522, 15522, 15522, 15522, 15522, 15522, 15522, 15522, 15522, 15522, 15522, 15522, 15553, 15553, 15553, 15553, 15553, 15553, 15553, 15553, 15553, 15553, 15553, 15553), class = "Date"), variable = c("b", "bc", "f", "in", "it", "l", "of", "o", "pr", "s", "total", "tr", "b", "bc", "f", "in", "it", "l", "of", "o", "pr", "s", "total", "tr", "b", "bc", "f", "in", "it", "l", "of", "o", "pr", "s", "total", "tr", "b", "bc", "f", "in", "it", "l", "of", "o", "pr", "s", "total", "tr", "b", "bc", "f", "in", "it", "l", "of", "o", "pr", "s", "total", "tr", "b", "bc", "f", "in", "it", "l", "of", "o", "pr", "s", "total", "tr", "b", "bc", "f", "in", "it", "l", "of", "o", "pr", "s", "total", "tr", "b", "bc", "f", "in", "it", "l", "of", "o", "pr", "s", "total", "tr"), value = c(-23, 6.90000000000001, 459.799999999999, -403.6, -56.1, -95, -13.8, 32.6, 121.5, -15.7, 26.2000000000007, 12.5, -25.1, 238.3, 1047.2, -803.2, -151.5, -260.5, -59.6, -93.8, 461.5, -37.7, 26.7999999999993, -288.8, -46.4, 249, 1289.8, -783.2, -188.1, -414.9, -77.7, -61, 928.4, -36.8, 17.4000000000015, -841.7, -46.5, 276.2, 1384.8, -541.1, -71.8999999999999, -433.3, -61.3, -28.3, 494.699999999999, -23.4, -14.5999999999985, -964.5, -46.1, 376.2, 1020.1, -119.4, 56.8000000000001, -447.7, -9.50000000000001, 14.2, -9.20000000000164, 2.5, -42.7999999999993, -880.6, -52.9, 345.5, 892.599999999999, -241.8, 144.3, -428.2, -3.30000000000001, 91.9, -294.800000000002, -5.19999999999999, -42.1999999999971, -490.1, -64.5, 379.7, 679.299999999999, -143.1, 185.9, -419.8, -4.30000000000001, 182.4, -421.900000000002, 1.80000000000001, -59.8999999999978, -435.2, -80.2, 422.2, 645.499999999998, -391.4, 76.6000000000001, -387.4, -1.70000000000001, 211.2, -131.500000000002, -10.6, -40.8999999999978, -393.6), fill = c("#A4D3EE80", "#A478AB80", "#01AEF080", "#8DC73F80", "#F8931D80", "#FFAAAA80", "#8C8C8C", "#D38D5F80", "#23238E80", "#77B9B780", "#C8373780", "#EEDD8280", "#A4D3EE80", "#A478AB80", "#01AEF080", "#8DC73F80", "#F8931D80", "#FFAAAA80", "#8C8C8C", "#D38D5F80", "#23238E80", "#77B9B780", "#C8373780", "#EEDD8280", "#A4D3EE80", "#A478AB80", "#01AEF080", "#8DC73F80", "#F8931D80", "#FFAAAA80", "#8C8C8C", "#D38D5F80", "#23238E80", "#77B9B780", "#C8373780", "#EEDD8280", "#A4D3EE80", "#A478AB80", "#01AEF080", "#8DC73F80", "#F8931D80", "#FFAAAA80", "#8C8C8C", "#D38D5F80", "#23238E80", "#77B9B780", "#C8373780", "#EEDD8280", "#A4D3EE80", "#A478AB80", "#01AEF080", "#8DC73F80", "#F8931D80", "#FFAAAA80", "#8C8C8C", "#D38D5F80", "#23238E80", "#77B9B780", "#C8373780", "#EEDD8280", "#A4D3EE80", "#A478AB80", "#01AEF080", "#8DC73F80", "#F8931D80", "#FFAAAA80", "#8C8C8C", "#D38D5F80", "#23238E80", "#77B9B780", "#C8373780", "#EEDD8280", "#A4D3EE80", "#A478AB80", "#01AEF080", "#8DC73F80", "#F8931D80", "#FFAAAA80", "#8C8C8C", "#D38D5F80", "#23238E80", "#77B9B780", "#C8373780", "#EEDD8280", "#A4D3EE80", "#A478AB80", "#01AEF080", "#8DC73F80", "#F8931D80", "#FFAAAA80", "#8C8C8C", "#D38D5F80", "#23238E80", "#77B9B780", "#C8373780", "#EEDD8280")), .Names = c("mydate", "variable", "value", "fill"), row.names = c(NA, 96L), class = "data.frame")

myvals <- mymelt[mymelt$mydate == mymelt$mydate[nrow(mymelt)],] ## last date in mymelt should always be same as plotenddate as we subset earlier
mymelt <- within(mymelt, variable <- factor(variable, as.character(myvals[order(myvals$value, decreasing = T),]$variable), ordered = TRUE))

p <- ggplot(mymelt, aes(x = mydate, y = value)) +
    geom_line(lwd=0.3) +
    facet_grid(. ~ variable) +
    theme(axis.text.x = element_text(size = 5, angle = 90),
          axis.text.y = element_text(size = 8),
          axis.title.x = element_text(vjust = 0),
          axis.ticks = element_blank(),
          panel.grid.minor = element_blank())

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="facetgrid/timeseries")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4239.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Geom Line


```r
library(plotly)
library(plyr)

date <- rep(as.Date(1:365,origin='2011-1-1'),7)
location <- factor(rep(1:7,365))
product <- rep(letters[1:7], each=365)
value <- c(sample(1:10, size=365, replace=T),sample(1:3, size=365, replace=T),
           sample(10:100, size=365, replace=T), sample(1:50, size=365, replace=T),
           sample(1:20, size=365, replace=T),sample(50:100, size=365, replace=T),
           sample(1:100, size=365, replace=T))
dat<-data.frame(date,location,product,value)

corr_dat <- ddply(dat, .(product, value), summarise)
```

```
## Error: length(rows) == 1 is not TRUE
```

```r
corr.df<-unstack(corr_dat, value~product)
```

```
## Error in unstack(corr_dat, value ~ product): object 'corr_dat' not found
```

```r
corr_plot <- data.frame(date=max(dat$date),
                        label=paste0("rho==",round(cor(corr.df)[,1], 2)),
                        ddply(dat, .(product), summarise,
                              value=(min(value)+max(value))/2))
```

```
## Error in is.data.frame(x): object 'corr.df' not found
```

```r
p <- ggplot(dat, aes(x=date, y=value, color=location, group=location)) +
    geom_line()+
    facet_grid(product ~ ., scale = "free_y")

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="facetgrid/geomline")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4241.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>
