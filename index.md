---
title: "Developing Data Product"
subtitle: "Week 3 Assignment"
author: "Nur Seto Dimas"
date: "1 January 2020"
output: 
  ioslides_presentation: 
    highlight: haddock
    keep_md: yes
    smaller: yes
---



## Overview  
This is an R Markdown presentation about global suicide rates in 1985 to 2016. The dataset is from [kaggle](https://www.kaggle.com/russellyates88/suicide-rates-overview-1985-to-2016).  

## References
- United Nations Development Program. (2018). Human development index (HDI). Retrieved from http://hdr.undp.org/en/indicators/137506

- World Bank. (2018). World development indicators: GDP (current US$) by country:1985 to 2016. Retrieved from http://databank.worldbank.org/data/source/world-development-indicators#

- [Szamil]. (2017). Suicide in the Twenty-First Century [dataset]. Retrieved from https://www.kaggle.com/szamil/suicide-in-the-twenty-first-century/notebook

- World Health Organization. (2018). Suicide prevention. Retrieved from http://www.who.int/mental_health/suicide-prevention/en/ 



## Data Preprocessing

```r
library(tidyverse)
library(plotly)

# load dataset
plotdata <- read.csv(file = "master.csv")

# tidying up dataset
plotdata <- plotdata %>% 
        rename(country.name = ï..country) %>%
        as.data.frame()

plotdata_summary <- plotdata %>%
        group_by(year) %>%
        summarize(population = sum(population),
                  suicides = sum(suicides_no),
                  suicides_per_100k = (suicides / population) * 100000)
```


## Plotly

```r
# Create plot
p <- plot_ly(data = plotdata_summary, 
             x = ~year, y = ~suicides_per_100k, 
             mode = "lines+markers") %>%
        layout(title = "Global Suicides Trends per 100k")
```

## Plotly
<!--html_preserve--><div id="htmlwidget-268f26d022be426987ad" style="width:720px;height:432px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-268f26d022be426987ad">{"x":{"visdat":{"1ba87546119b":["function () ","plotlyVisDat"]},"cur_data":"1ba87546119b","attrs":{"1ba87546119b":{"x":{},"y":{},"mode":"lines+markers","alpha_stroke":1,"sizes":[10,100],"spans":[1,20]}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"title":"Global Suicides Trends per 100k","xaxis":{"domain":[0,1],"automargin":true,"title":"year"},"yaxis":{"domain":[0,1],"automargin":true,"title":"suicides_per_100k"},"hovermode":"closest","showlegend":false},"source":"A","config":{"showSendToCloud":false},"data":[{"x":[1985,1986,1987,1988,1989,1990,1991,1992,1993,1994,1995,1996,1997,1998,1999,2000,2001,2002,2003,2004,2005,2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016],"y":[11.5073359214447,11.7165621601009,11.5834298364974,11.4815141076963,13.0756527161244,13.1841231413643,13.2900364946738,13.4735702504456,14.4774300136439,14.9838963098543,15.302227830618,14.8426758000662,14.136594182299,14.467522492944,14.4181666501634,14.2189879815937,14.277564783002,14.0545292300306,13.9290099210424,13.8009722067858,13.5093490704526,12.6764017484044,12.551757061994,12.6542169982379,12.3207926871747,11.9512501485952,11.8635732301979,12.0325462936953,11.808460557589,11.6619935474957,11.4748874319967,11.8113369091992],"mode":"lines+markers","type":"scatter","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"error_y":{"color":"rgba(31,119,180,1)"},"error_x":{"color":"rgba(31,119,180,1)"},"line":{"color":"rgba(31,119,180,1)"},"xaxis":"x","yaxis":"y","frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->
