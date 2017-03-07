---
name: Static Image Export
permalink: r/static-image-export/
description: How to export plotly graphs as static images in R. Plotly supports png, svg, jpg, and pdf image export.
layout: base
thumbnail: thumbnail/png-export.png
language: r
page_type: example_index
has_thumbnail: true
order: 2
display_as: file_settings
sitemap: false
output:
  html_document:
    keep_md: true
---

Recent versions of the R package include an `export()` function, which does image export locally, but requires the webshot package:


```r
if (!require("webshot")) install.packages("webshot")
tmpFile <- tempfile(fileext = ".png")
export(plot_ly(), file = tmpFile)
browseURL(tmpFile)
```

Another option is to do image export through your plotly account. First, if you haven't already, let the R package know about your credentials


```r
Sys.setenv("plotly_username" = "YOUR USER NAME")
Sys.setenv("plotly_api_key" = "YOUR API KEY")
```


```r
library(plotly)
```

```
## Loading required package: ggplot2
```

```
## Warning: package 'ggplot2' was built under R version 3.3.2
```

```
##
## Attaching package: 'plotly'
```

```
## The following object is masked from 'package:ggplot2':
##
##     last_plot
```

```
## The following object is masked from 'package:stats':
##
##     filter
```

```
## The following object is masked from 'package:graphics':
##
##     layout
```

```r
p <- plot_ly(x = 1, y = 1, type = 'scatter', mode = 'markers')
plotly_IMAGE(p, format = "png", out_file = "output.png")
```

This will export the image on plotly's servers and write the content to a local file `"output.png"` in your working directory.

You can also view the static version of any Plotly graph by appending `.png`,
`.pdf`, `.eps`, or `.svg` to the end of the URL. For example, view the static image of <https://plot.ly/~chris/1638> at <https://plot.ly/~chris/1638.png>. See [Using Plotly with rmarkdown/knitr](https://plot.ly/r/knitr/) for a way to embed these links in rmarkdown/knitr (Rmd) files.