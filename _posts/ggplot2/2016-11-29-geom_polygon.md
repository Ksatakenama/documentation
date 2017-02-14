---
title: geom_polygon | Examples | Plotly
name: geom_polygon
permalink: ggplot2/geom_polygon/
description: Examples of geom_polygon in R.
layout: base
thumbnail: thumbnail/shape.jpg
language: ggplot2
page_type: example_index
has_thumbnail: true
display_as: basic
order: 7
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

### Basic Ploygon


```r
library(plotly)

ids <- factor(c("1.1", "2.1", "1.2", "2.2", "1.3", "2.3"))

values <- data.frame(
  id = ids,
  value = c(3, 3.1, 3.1, 3.2, 3.15, 3.5)
)

positions <- data.frame(
  id = rep(ids, each = 4),
  x = c(2, 1, 1.1, 2.2, 1, 0, 0.3, 1.1, 2.2, 1.1, 1.2, 2.5, 1.1, 0.3,
  0.5, 1.2, 2.5, 1.2, 1.3, 2.7, 1.2, 0.5, 0.6, 1.3),
  y = c(-0.5, 0, 1, 0.5, 0, 0.5, 1.5, 1, 0.5, 1, 2.1, 1.7, 1, 1.5,
  2.2, 2.1, 1.7, 2.1, 3.2, 2.8, 2.1, 2.2, 3.3, 3.2)
)

datapoly <- merge(values, positions, by=c("id"))

p <- ggplot(datapoly, aes(x=x, y=y)) + geom_polygon(aes(fill=value, group=id))

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_polygon/basic")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4147.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>
Inspired by <a href="http://docs.ggplot2.org/current/geom_polygon.html">ggplot2 docs</a>

### Ellipses


```r
# create data
set.seed(20130226)
n <- 200
x1 <- rnorm(n, mean = 2)
y1 <- 1.5 + 0.4 * x1 + rnorm(n)
x2 <- rnorm(n, mean = -1)
y2 <- 3.5 - 1.2 * x2 + rnorm(n)
class <- rep(c("A", "B"), each = n)
df <- data.frame(x = c(x1, x2), y = c(y1, y2), colour = class)

# get code for "stat_ellipse"
library(devtools)
library(ggplot2)
library(proto) #source_url("https://raw.github.com/JoFrhwld/FAAV/master/r/stat-ellipse.R")

p <- qplot(data = df, x = x, y = y, colour = class) +
  stat_ellipse(geom = "polygon", alpha = 1/2, aes(fill = class))

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_polygon/ellipses")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4149.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Highlighting


```r
library(plotly)

tmp <- with(mtcars, data.frame(x=c(0, 0, max(wt)*35), y=c(0, max(wt), max(wt))))

p <- ggplot(mtcars, aes(hp, wt)) +
  geom_polygon(data=tmp, aes(x, y), fill="#d8161688") +
  geom_point()

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_polygon/highlight")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4151.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>
Inspired by <a href="http://stackoverflow.com/questions/3610291/highlighting-regions-of-interest-in-ggplot2/3610506#3610506">Stack Overflow</a>

### Vertical Conversion


```r
library(plotly)

library(data.table)
df<-data.table(Product=letters[1:10], minX=1:10, maxX=5:14, minY= 10:1, maxY=14:5)

df.t<-data.table(rbind( df[,list(Product,X=minX,Y=minY)],
       df[,list(Product,X=minX,Y=maxY)],
       df[,list(Product,X=maxX,Y=minY)],
       df[,list(Product,X=maxX,Y=maxY)]))[
      order(Product,X,Y)]

p <- ggplot(df,aes(xmin=minX,xmax=maxX,ymin=minY,ymax=maxY,fill=Product))+
  geom_rect()

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_polygon/vertical")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4153.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>
Inspired by <a href="http://stackoverflow.com/questions/22100486/r-ggplot2-convert-row-records-to-vertical-values-and-use-in-geom-polygon">Stack Overflow</a>

### Distributions


```r
library(plotly)

x=seq(-2,2,length=200)
dat <- data.frame(
  norm = dnorm(x,mean=0,sd=0.2),
  logistic = dlogis(x,location=0,scale=0.2), x = x
)
p <- ggplot(data=dat, aes(x=x)) +
  geom_polygon(aes(y=norm), fill="red", alpha=0.6) +
  geom_polygon(aes(y=logistic), fill="blue", alpha=0.6) +
  xlab("z") + ylab("") +
  scale_x_continuous(expand = c(0, 0)) +
  scale_y_continuous(expand = c(0, 0))

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_polygon/distributions")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4155.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>
Inspired by <a href="http://stackoverflow.com/questions/7474106/geom-polygon-to-draw-normal-and-logistic-distributions">Stack Overflow</a>

### Convex Hull


```r
library(plotly)

doInstall <- TRUE  # Change to FALSE if you don't want packages installed.
toInstall <- c("RColorBrewer")
if(doInstall){install.packages(toInstall, repos = "http://cran.us.r-project.org")}
lapply(toInstall, library, character.only = TRUE)

# Generate some data
nn <- 500
myData <- data.frame(X = rnorm(nn),
                     Y = rnorm(nn))

setK = 6  # How many clusters?
clusterSolution <- kmeans(myData, centers = setK)

myData$whichCluster <- factor(clusterSolution$cluster)

splitData <- split(myData, myData$whichCluster)
appliedData <- lapply(splitData, function(df){
  df[chull(df), ]  # chull really is useful, even outside of contrived examples.
  })
combinedData <- do.call(rbind, appliedData)

zp3 <- ggplot(data = myData,
                     aes(x = X, y = Y))
zp3 <- zp3 + geom_polygon(data = combinedData,  # This is also a nice example of how to plot
                          aes(x = X, y = Y, fill = whichCluster),  # two superimposed geoms
                          alpha = 1/2)                             # from different data.frames
zp3 <- zp3 + geom_point(size=1)
zp3 <- zp3 + coord_equal()
zp3 <- zp3 + scale_fill_manual(values = colorRampPalette(rev(brewer.pal(11, "Spectral")))(setK))

p <- ggplotly(zp3)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_polygon/convex")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4157.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>
Inspired by <a href="http://is-r.tumblr.com/post/33356702763/from-holey-polygons-to-convex-hulls">is.R()</a>

### Maps


```r
library(plotly)
library(plyr)
library(maps)
library(mapproj)
```

```
## Error in library(mapproj): there is no package called 'mapproj'
```

```r
us_ag <- 
  read.csv("https://raw.githubusercontent.com/plotly/datasets/master/2011_us_ag_exports.csv")

df <- subset(us_ag, select=c(state,total.veggies))

# state names to lowercase
df$region <- tolower(df$state)

# map data
us_state_map <- map_data('state')
map_data <- merge(df, us_state_map, by = 'region')
map_data <- arrange(map_data, order)

states <- data.frame(state.center, state.abb)

p <- ggplot(data = map_data, aes(x = long, y = lat, group = group)) + 
  geom_polygon(aes(fill = cut_number(total.veggies, 5))) + 
  geom_path(colour = 'gray') + 
  scale_fill_brewer('Total Veggie Export (2011)', palette  = 'PuRd') + 
  coord_map() + 
  theme_bw()

p <- ggplotly(p)
```

```
## Error in loadNamespace(name): there is no package called 'mapproj'
```

```r
# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="geom_polygon/maps")
```

```
## Error in loadNamespace(name): there is no package called 'mapproj'
```

```r
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4157.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>
