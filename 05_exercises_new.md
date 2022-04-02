---
title: 'Weekly Exercises #5'
author: "Emanuel Deleon Otazu"
output: 
  html_document:
    keep_md: TRUE
    toc: TRUE
    toc_float: TRUE
    df_print: paged
    code_download: true
---





```r
library(tidyverse)     # for data cleaning and plotting
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──
```

```
## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
## ✓ tibble  3.1.6     ✓ dplyr   1.0.8
## ✓ tidyr   1.2.0     ✓ stringr 1.4.0
## ✓ readr   2.1.2     ✓ forcats 0.5.1
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(gardenR)       # for Lisa's garden data
library(lubridate)     # for date manipulation
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following objects are masked from 'package:base':
## 
##     date, intersect, setdiff, union
```

```r
library(openintro)     # for the abbr2state() function
```

```
## Loading required package: airports
```

```
## Loading required package: cherryblossom
```

```
## Loading required package: usdata
```

```r
library(palmerpenguins)# for Palmer penguin data
library(maps)          # for map data
```

```
## 
## Attaching package: 'maps'
```

```
## The following object is masked from 'package:purrr':
## 
##     map
```

```r
library(ggmap)         # for mapping points on maps
```

```
## Google's Terms of Service: https://cloud.google.com/maps-platform/terms/.
```

```
## Please cite ggmap if you use it! See citation("ggmap") for details.
```

```r
library(gplots)        # for col2hex() function
```

```
## 
## Attaching package: 'gplots'
```

```
## The following object is masked from 'package:stats':
## 
##     lowess
```

```r
library(RColorBrewer)  # for color palettes
library(sf)            # for working with spatial data
```

```
## Linking to GEOS 3.9.1, GDAL 3.4.0, PROJ 8.1.1; sf_use_s2() is TRUE
```

```r
library(leaflet)       # for highly customizable mapping
library(ggthemes)      # for more themes (including theme_map())
library(plotly)        # for the ggplotly() - basic interactivity
```

```
## 
## Attaching package: 'plotly'
```

```
## The following object is masked from 'package:ggmap':
## 
##     wind
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
library(gganimate)     # for adding animation layers to ggplots
library(transformr)    # for "tweening" (gganimate)
```

```
## 
## Attaching package: 'transformr'
```

```
## The following object is masked from 'package:sf':
## 
##     st_normalize
```

```r
library(gifski)        # need the library for creating gifs but don't need to load each time
library(shiny)         # for creating interactive apps
theme_set(theme_minimal())
library(babynames)
```

```
## 
## Attaching package: 'babynames'
```

```
## The following object is masked from 'package:openintro':
## 
##     births
```


```r
# SNCF Train data
small_trains <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-02-26/small_trains.csv") 
```

```
## Rows: 32772 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (4): service, departure_station, arrival_station, delay_cause
## dbl (9): year, month, journey_time_avg, total_num_trips, avg_delay_all_depar...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
# Lisa's garden data
data("garden_harvest")

# Lisa's Mallorca cycling data
mallorca_bike_day7 <- read_csv("https://www.dropbox.com/s/zc6jan4ltmjtvy0/mallorca_bike_day7.csv?dl=1") %>% 
  select(1:4, speed)
```

```
## Rows: 3210 Columns: 11
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## dbl  (8): lon, lat, ele, extensions, ele.num, time_hr, dist_km, speed
## dttm (2): time, hrminsec
## date (1): date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
# Heather Lendway's Ironman 70.3 Pan Am championships Panama data
panama_swim <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_swim_20160131.csv")
```

```
## Rows: 36 Columns: 8
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (1): event
## dbl  (3): lon, lat, extensions
## lgl  (1): ele
## dttm (2): time, hrminsec
## date (1): date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
panama_bike <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_bike_20160131.csv")
```

```
## Rows: 7924 Columns: 8
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (1): event
## dbl  (4): lon, lat, ele, extensions
## dttm (2): time, hrminsec
## date (1): date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
panama_run <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_run_20160131.csv")
```

```
## Rows: 1111 Columns: 8
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (1): event
## dbl  (4): lon, lat, ele, extensions
## dttm (2): time, hrminsec
## date (1): date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
#COVID-19 data from the New York Times
covid19 <- read_csv("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv")
```

```
## Rows: 41894 Columns: 5
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (2): state, fips
## dbl  (2): cases, deaths
## date (1): date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```



## Warm-up exercises from tutorial

  1. Choose 2 graphs you have created for ANY assignment in this class and add interactivity using the `ggplotly()` function.
  
```{r, fig.alt= "barplot showing the popularity of the name Emanuel over time.There is a constant increase starting in 1979 and in 2007 the popularity started to decrease}"
emanuel_popularity <- babynames %>% 
  filter(sex == "M") %>% 
  filter(name %in% c ("Emanuel")) %>% 
  group_by( name, year) %>% 
  arrange(desc(n)) %>% 
  ungroup() %>% 
ggplot(aes( x = year,
            y = n))+
geom_col(color = "darkblue")+
  labs(title = "Popularity of the name 'Emanuel' over time ",
       x = "",
       y = "",
       caption ="Data from the US and New Zealand,
                Source: USA social security administration ")+
  theme_clean()

ggplotly(emanuel_popularity,
         tooltip = c("text", "x")) 

  

```r
tomatoes_2020 <-garden_harvest %>% 
  filter( vegetable == "tomatoes") %>% 
  group_by(date) %>% 
  mutate(weight_lbs = weight*0.00220462) %>% 
  summarise(total_weight_lbs = sum(weight_lbs)) %>%  
ggplot(aes(y = total_weight_lbs, x = date, color = variety))+
  geom_line(color = "darkblue")+
  labs( x= "",
        y =  "",
        title = "The amount of tomatoes harvested by day in pounds during 2020",
       caption = "Graph by Emanuel Deleon Otazu") +
  theme(plot.title = element_text(hjust = 0.5))+
  theme_clean()

ggplotly(tomatoes_2020, 
         tooltip = c("text", "x"))
```

```{=html}
<div id="htmlwidget-b0f5943fc9d3c6c5d295" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-b0f5943fc9d3c6c5d295">{"x":{"data":[{"x":[18454,18464,18467,18468,18469,18470,18471,18472,18473,18474,18475,18476,18477,18478,18479,18480,18481,18482,18483,18484,18485,18487,18488,18490,18491,18492,18493,18494,18495,18497,18498,18499,18500,18503,18504,18506,18508,18509,18511,18515,18520,18522,18523,18524,18526,18530,18535,18538,18542,18545,18546,18549],"y":[0.05291088,1.23899644,1.40654756,1.25442878,0.32628376,1.76590062,3.46566264,2.38980808,0.20062042,3.36645474,4.5745865,4.78623002,0.67902296,2.53090376,5.56225626,2.59704236,7.07903482,2.18477842,5.06621676,1.00751134,6.63149696,5.5887117,5.59312094,7.56846046,6.09136506,3.4943227,9.74221578,8.5649487,12.80663758,12.72286202,0.1653465,14.56371972,13.86485518,8.40621606,18.51439876,14.65851838,6.62708772,18.95532276,14.70040616,10.471945,2.16714146,0.46737944,9.4688429,9.47104752,1.78353758,26.4003245,6.64913392,1.78794682,3.67730616,7.39429548,11.92478958,16.3803266],"text":["date: 2020-07-11","date: 2020-07-21","date: 2020-07-24","date: 2020-07-25","date: 2020-07-26","date: 2020-07-27","date: 2020-07-28","date: 2020-07-29","date: 2020-07-30","date: 2020-07-31","date: 2020-08-01","date: 2020-08-02","date: 2020-08-03","date: 2020-08-04","date: 2020-08-05","date: 2020-08-06","date: 2020-08-07","date: 2020-08-08","date: 2020-08-09","date: 2020-08-10","date: 2020-08-11","date: 2020-08-13","date: 2020-08-14","date: 2020-08-16","date: 2020-08-17","date: 2020-08-18","date: 2020-08-19","date: 2020-08-20","date: 2020-08-21","date: 2020-08-23","date: 2020-08-24","date: 2020-08-25","date: 2020-08-26","date: 2020-08-29","date: 2020-08-30","date: 2020-09-01","date: 2020-09-03","date: 2020-09-04","date: 2020-09-06","date: 2020-09-10","date: 2020-09-15","date: 2020-09-17","date: 2020-09-18","date: 2020-09-19","date: 2020-09-21","date: 2020-09-25","date: 2020-09-30","date: 2020-10-03","date: 2020-10-07","date: 2020-10-10","date: 2020-10-11","date: 2020-10-14"],"type":"scatter","mode":"lines","line":{"width":1.88976377952756,"color":"rgba(0,0,139,1)","dash":"solid"},"hoveron":"points","showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":45.7550850975509,"r":7.97011207970112,"b":27.0983810709838,"l":23.9103362391034},"paper_bgcolor":"rgba(255,255,255,1)","font":{"color":"rgba(0,0,0,1)","family":"sans","size":15.9402241594022},"title":{"text":"<b> The amount of tomatoes harvested by day in pounds during 2020 <\/b>","font":{"color":"rgba(0,0,0,1)","family":"sans","size":18.5969281859693},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[18449.25,18553.75],"tickmode":"array","ticktext":["Aug","Sep","Oct"],"tickvals":[18475,18506,18536],"categoryorder":"array","categoryarray":["Aug","Sep","Oct"],"nticks":null,"ticks":"outside","tickcolor":"rgba(0,0,0,1)","ticklen":3.98505603985056,"tickwidth":0.724555643609193,"showticklabels":true,"tickfont":{"color":"rgba(0,0,0,1)","family":"sans","size":11.9551681195517},"tickangle":-0,"showline":true,"linecolor":"rgba(0,0,0,1)","linewidth":0.66417600664176,"showgrid":false,"gridcolor":null,"gridwidth":0,"zeroline":false,"anchor":"y","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"sans","size":13.2835201328352}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-1.264459801,27.717695181],"tickmode":"array","ticktext":["0","10","20"],"tickvals":[0,10,20],"categoryorder":"array","categoryarray":["0","10","20"],"nticks":null,"ticks":"outside","tickcolor":"rgba(0,0,0,1)","ticklen":3.98505603985056,"tickwidth":0.724555643609193,"showticklabels":true,"tickfont":{"color":"rgba(0,0,0,1)","family":"sans","size":11.9551681195517},"tickangle":-0,"showline":true,"linecolor":"rgba(0,0,0,1)","linewidth":0.66417600664176,"showgrid":true,"gridcolor":"rgba(190,190,190,1)","gridwidth":0.724555643609193,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"sans","size":13.2835201328352}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":"rgba(255,255,255,1)","bordercolor":"rgba(0,0,0,1)","borderwidth":2.06156048675734,"font":{"color":"rgba(0,0,0,1)","family":"sans","size":14.6118721461187}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"source":"A","attrs":{"c1ac4e9994cd":{"x":{},"y":{},"colour":{},"type":"scatter"}},"cur_data":"c1ac4e9994cd","visdat":{"c1ac4e9994cd":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```

  
  2. Use animation to tell an interesting story with the `small_trains` dataset that contains data from the SNCF (National Society of French Railways). These are Tidy Tuesday data! Read more about it [here](https://github.com/rfordatascience/tidytuesday/tree/master/data/2019/2019-02-26).
  
  #total number of international trips over time 
  #filter only to international services 
  #total number of trips 


```r
small_trains %>% 
  filter(service == "International") %>% 
  group_by(year) %>% 
  summarise(total_trips_year = sum(total_num_trips)) %>% 
  ggplot(aes(x = year, y = total_trips_year, color = year))+
  geom_line()+
  labs(title = "Quantity of International trips by year",
       subtitle = "year: {frame_along}",
       x = "",
       y = "",
       color = "year") +
  transition_reveal(year)
```

<img src="05_exercises_new_files/figure-html/unnamed-chunk-2-1.gif" title="Animated line graph showing the quantity of international trips by year. There is a decrease in the quantity starting in 2015 and in 2016 in starts to increase again" alt="Animated line graph showing the quantity of international trips by year. There is a decrease in the quantity starting in 2015 and in 2016 in starts to increase again"  />

```r
anim_save("small_trains.gif")
knitr::include_graphics("small_trains.gif")
```

<img src="small_trains.gif" title="Animated line graph showing the quantity of international trips by year. There is a decrease in the quantity starting in 2015 and in 2016 in starts to increase again" alt="Animated line graph showing the quantity of international trips by year. There is a decrease in the quantity starting in 2015 and in 2016 in starts to increase again"  />


## Garden data

  3. In this exercise, you will create a stacked area plot that reveals itself over time (see the `geom_area()` examples [here](https://ggplot2.tidyverse.org/reference/position_stack.html)). You will look at cumulative harvest of tomato varieties over time. I have filtered the data to the tomatoes and find the *daily* harvest in pounds for each variety. The `complete()` function creates a row for all unique `date`/`variety` combinations. If a variety is not harvested on one of the harvest dates in the dataset, it is filled with a value of 0. 
  You should do the following:
  * For each variety, find the cumulative harvest in pounds.  
  * Use the data you just made to create a static cumulative harvest area plot, with the areas filled with different colors for each variety and arranged (HINT: `fct_reorder()`) from most to least harvested weights (most on the bottom).  
  * Add animation to reveal the plot over date. Instead of having a legend, place the variety names directly on the graph (refer back to the tutorial for how to do this).


```r
garden_harvest %>% 
  filter(vegetable == "tomatoes") %>% 
  group_by(date, variety) %>% 
  summarize(daily_harvest_lb = sum(weight)*0.00220462) %>% 
  ungroup() %>% 
  complete(variety, 
           date, 
           fill = list(daily_harvest_lb = 0)) %>% 
  mutate(variety = fct_reorder(variety,daily_harvest_lb, sum)) %>% 
  group_by(variety) %>% 
  mutate(cum_variety_harvest =cumsum(daily_harvest_lb))  %>% 
  ggplot(aes(x = date, 
             y = cum_variety_harvest , 
             fill = (variety)))+
  geom_area()+
  geom_text (aes(label = variety), position = "stack") +
  labs(title = "Cumulative harvest of tomato varieties over time",
       subtitle = "Date: {frame_along}",
       x = "",
       y = "")+
  transition_reveal(date)+
  theme(legend.position = "none")
```

```
## `summarise()` has grouped output by 'date'. You can override using the
## `.groups` argument.
```

<img src="05_exercises_new_files/figure-html/unnamed-chunk-3-1.gif" title="stacked area plot that shows the Cumulative harvest of tomato varieties over time" alt="stacked area plot that shows the Cumulative harvest of tomato varieties over time"  />

```r
anim_save("harvest_tomato.gif")
knitr::include_graphics("harvest_tomato.gif")
```

<img src="harvest_tomato.gif" title="stacked area plot that shows the Cumulative harvest of tomato varieties over time" alt="stacked area plot that shows the Cumulative harvest of tomato varieties over time"  />


## Maps, animation, and movement!

  4. Map Lisa's `mallorca_bike_day7` bike ride using animation! 
  Requirements:
  * Plot on a map using `ggmap`.  
  * Show "current" location with a red point. 
  * Show path up until the current point.  
  * Color the path according to elevation.  
  * Show the time in the subtitle.  
  * CHALLENGE: use the `ggimage` package and `geom_image` to add a bike image instead of a red point. You can use [this](https://raw.githubusercontent.com/llendway/animation_and_interactivity/master/bike.png) image. See [here](https://goodekat.github.io/presentations/2019-isugg-gganimate-spooky/slides.html#35) for an example. 
  * Add something of your own! And comment on if you prefer this to the static map and why or why not.
  

```r
mallorca_map <- get_stamenmap(
    bbox = c( left = 2.28 , bottom = 39.41 , right = 3.03 , top = 39.8 ), 
    maptype = "terrain",
    zoom = 11)
```

```
## Source : http://tile.stamen.com/terrain/11/1036/776.png
```

```
## Source : http://tile.stamen.com/terrain/11/1037/776.png
```

```
## Source : http://tile.stamen.com/terrain/11/1038/776.png
```

```
## Source : http://tile.stamen.com/terrain/11/1039/776.png
```

```
## Source : http://tile.stamen.com/terrain/11/1040/776.png
```

```
## Source : http://tile.stamen.com/terrain/11/1041/776.png
```

```
## Source : http://tile.stamen.com/terrain/11/1036/777.png
```

```
## Source : http://tile.stamen.com/terrain/11/1037/777.png
```

```
## Source : http://tile.stamen.com/terrain/11/1038/777.png
```

```
## Source : http://tile.stamen.com/terrain/11/1039/777.png
```

```
## Source : http://tile.stamen.com/terrain/11/1040/777.png
```

```
## Source : http://tile.stamen.com/terrain/11/1041/777.png
```

```
## Source : http://tile.stamen.com/terrain/11/1036/778.png
```

```
## Source : http://tile.stamen.com/terrain/11/1037/778.png
```

```
## Source : http://tile.stamen.com/terrain/11/1038/778.png
```

```
## Source : http://tile.stamen.com/terrain/11/1039/778.png
```

```
## Source : http://tile.stamen.com/terrain/11/1040/778.png
```

```
## Source : http://tile.stamen.com/terrain/11/1041/778.png
```

```
## Source : http://tile.stamen.com/terrain/11/1036/779.png
```

```
## Source : http://tile.stamen.com/terrain/11/1037/779.png
```

```
## Source : http://tile.stamen.com/terrain/11/1038/779.png
```

```
## Source : http://tile.stamen.com/terrain/11/1039/779.png
```

```
## Source : http://tile.stamen.com/terrain/11/1040/779.png
```

```
## Source : http://tile.stamen.com/terrain/11/1041/779.png
```

```r
ggmap(mallorca_map) +
  geom_point(data = mallorca_bike_day7,
             aes(x = lon, y = lat),
             zoom = .5) + 
  geom_path(data = mallorca_bike_day7 , 
             aes(x = lon  , y = lat  , color = ele ),
             size = .3) +
  annotate(geom = "point", y = 39.66002, x = 2.586712, color = "darkred", size = 3)+
  annotate(geom = "text", y = 39.66002, x = 2.586712, label = "current", size = 2)+
  theme(legend.background = element_blank())+
  labs(title = "Lisa's Mallorca bike ride",
       subtitle = "Time: {frame_along}",
       color = "Elevation") +
  scale_color_viridis_c(option = "magma" ) +
  transition_reveal(time) +
  theme_map()
```

```
## Warning: Ignoring unknown parameters: zoom
```

<img src="05_exercises_new_files/figure-html/unnamed-chunk-4-1.gif" title="Map showing Lisa's bike ride in Mallorca- Spain with an animated line showing the trajectory" alt="Map showing Lisa's bike ride in Mallorca- Spain with an animated line showing the trajectory"  />

```r
anim_save("lisas_mallorca_bikeride.gif")
knitr::include_graphics("lisas_mallorca_bikeride.gif")
```

<img src="lisas_mallorca_bikeride.gif" title="Map showing Lisa's bike ride in Mallorca- Spain with an animated line showing the trajectory" alt="Map showing Lisa's bike ride in Mallorca- Spain with an animated line showing the trajectory"  />
  
  
  5. In this exercise, you get to meet Lisa's sister, Heather! She is a proud Mac grad, currently works as a Data Scientist where she uses R everyday, and for a few years (while still holding a full-time job) she was a pro triathlete. You are going to map one of her races. The data from each discipline of the Ironman 70.3 Pan Am championships, Panama is in a separate file - `panama_swim`, `panama_bike`, and `panama_run`. Create a similar map to the one you created with my cycling data. You will need to make some small changes: 1. combine the files putting them in swim, bike, run order (HINT: `bind_rows()`), 2. make the leading dot a different color depending on the event (for an extra challenge, make it a different image using `geom_image()!), 3. CHALLENGE (optional): color by speed, which you will need to compute on your own from the data. You can read Heather's race report [here](https://heatherlendway.com/2016/02/10/ironman-70-3-pan-american-championships-panama-race-report/). She is also in the Macalester Athletics [Hall of Fame](https://athletics.macalester.edu/honors/hall-of-fame/heather-lendway/184) and still has records at the pool. 
  

```r
panama <-bind_rows(panama_swim, panama_bike, panama_run)

panama_map <- get_stamenmap(
    bbox = c( left = -79.6901, bottom = 8.8590, right = -79.4041 , top = 9.0751), 
    maptype = "terrain",
    zoom = 7)
```

```
## Source : http://tile.stamen.com/terrain/7/35/60.png
```


```r
 ggmap(panama_map) +
  geom_point( data = panama,
              aes(x = lon, y = lat, color = event),
              size = 5)+
  geom_path(data = panama,
            aes(x = lon, y = lat),
            size = .8)+
  labs(title = "Heather's triathlon race in Panama",
       subtitle = "Time: {frame_along}",
       color = "event") +
  scale_color_viridis_d(option = "inferno" ) +
  transition_reveal(time) +
  theme_map()
```

![](05_exercises_new_files/figure-html/unnamed-chunk-6-1.gif)<!-- -->

```r
anim_save("heathers_race.gif")
knitr::include_graphics("heathers_race.gif")
```

![](heathers_race.gif)<!-- -->

  
## COVID-19 data

  6. In this exercise you will animate a map of the US, showing how cumulative COVID-19 cases per 10,000 residents has changed over time. This is similar to exercises 11 & 12 from the previous exercises, with the added animation! So, in the end, you should have something like the static map you made there, but animated over all the days. The code below gives the population estimates for each state and loads the `states_map` data. Here is a list of details you should include in the plot:
  
  * Put date in the subtitle.   
  * Because there are so many dates, you are going to only do the animation for the the 15th of each month. So, filter only to those dates - there are some lubridate functions that can help you do this.   
  * Use the `animate()` function to make the animation 200 frames instead of the default 100 and to pause for 10 frames on the end frame.   
  * Use `group = date` in `aes()`.   
  * Comment on what you see.  


```r
census_pop_est_2018 <- read_csv("https://www.dropbox.com/s/6txwv3b4ng7pepe/us_census_2018_state_pop_est.csv?dl=1") %>% 
  separate(state, into = c("dot","state"), extra = "merge") %>% 
  select(-dot) %>% 
  mutate(state = str_to_lower(state))
```

```
## Rows: 51 Columns: 2
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (1): state
## dbl (1): est_pop_2018
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
states_map <- map_data("state")

newer_cases <- covid19 %>% 
  arrange(desc(date)) %>% 
  group_by(state) %>% 
  mutate(numberrow = 1:n()) %>% 
  mutate(state = str_to_lower(`state`))

covid_population <- newer_cases %>% 
  left_join( census_pop_est_2018,
             by = c("state"="state")) %>% 
  mutate(covid_per_10000 = (cases/est_pop_2018)*10000)

covid_population %>% 
  filter(day(date) == 15) %>% 
  ggplot()+
  geom_map(map = states_map,
           aes(map_id = state,
               fill = covid_per_10000,
               group = date))+
  labs(title = "COVID-19 cases per 10,000 residents by date in the US",
       subtitle = "Date: {closest_state}",
       fill = "Cases per 10,000",
       caption = "")+
  expand_limits( x = states_map$long, y = states_map$lat)+
  scale_fill_viridis_c( option = "magma", direction = -1)+
  theme_map()+
  theme(legend.background = element_blank())+
  transition_states(date, transition_length = 0)
```

![](05_exercises_new_files/figure-html/unnamed-chunk-7-1.gif)<!-- -->

```r
anim_save("covid_cases.gif")
knitr::include_graphics("covid_cases.gif")
```

![](covid_cases.gif)<!-- -->

## Your first `shiny` app (for next week!)

  7. This app will also use the COVID data. Make sure you load that data and all the libraries you need in the `app.R` file you create. You should create a new project for the app, separate from the homework project. Below, you will post a link to the app that you publish on shinyapps.io. You will create an app to compare states' daily number of COVID cases per 100,000 over time. The x-axis will be date. You will have an input box where the user can choose which states to compare (`selectInput()`), a slider where the user can choose the date range, and a submit button to click once the user has chosen all states they're interested in comparing. The graph should display a different line for each state, with labels either on the graph or in a legend. Color can be used if needed. 
  
 
Put the link to your app here: https://edeleono.shinyapps.io/covid-app/
  
## GitHub link: https://github.com/rosde/covid-app

  8. Below, provide a link to your GitHub repo with this set of Weekly Exercises. 
  
https://github.com/rosde/exercise5 

**DID YOU REMEMBER TO UNCOMMENT THE OPTIONS AT THE TOP?**
