# Internet Subscriptions


```R
ict_stats <- read.csv("ict_stats.csv")
```


```R
str(ict_stats)
```

    'data.frame':	44 obs. of  4 variables:
     $ Year   : int  2011 2011 2011 2011 2012 2012 2012 2012 2013 2013 ...
     $ Quarter: chr  "Q1" "Q2" "Q3" "Q4" ...
     $ ADSL   : int  14082 14419 14474 15707 16298 17204 18166 18838 19388 23224 ...
     $ Mobile : int  189803 200198 224474 238942 263131 294548 509926 769805 958074 1098523 ...
    


```R
summary(ict_stats)
```


          Year        Quarter               ADSL            Mobile       
     Min.   :2011   Length:44          Min.   : 14082   Min.   : 189803  
     1st Qu.:2013   Class :character   1st Qu.: 24406   1st Qu.:1231656  
     Median :2016   Mode  :character   Median : 38898   Median :1426741  
     Mean   :2016                      Mean   : 43136   Mean   :1442396  
     3rd Qu.:2019                      3rd Qu.: 55572   3rd Qu.:1915367  
     Max.   :2021                      Max.   :101915   Max.   :2496146  



```R
ict_stats$Quarter <- as.factor(ict_stats$Quarter)
```


```R
head(ict_stats)
```


<table class="dataframe">
<caption>A data.frame: 6 × 4</caption>
<thead>
	<tr><th></th><th scope=col>Year</th><th scope=col>Quarter</th><th scope=col>ADSL</th><th scope=col>Mobile</th></tr>
	<tr><th></th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>2011</td><td>Q1</td><td>14082</td><td>189803</td></tr>
	<tr><th scope=row>2</th><td>2011</td><td>Q2</td><td>14419</td><td>200198</td></tr>
	<tr><th scope=row>3</th><td>2011</td><td>Q3</td><td>14474</td><td>224474</td></tr>
	<tr><th scope=row>4</th><td>2011</td><td>Q4</td><td>15707</td><td>238942</td></tr>
	<tr><th scope=row>5</th><td>2012</td><td>Q1</td><td>16298</td><td>263131</td></tr>
	<tr><th scope=row>6</th><td>2012</td><td>Q2</td><td>17204</td><td>294548</td></tr>
</tbody>
</table>




```R
library(dplyr)
library(viridis)
library(ggplot2)
library(plotly)
```


```R
g <- ggplot(ict_stats, aes(x = Year, y = ADSL, color = Quarter)) + 
geom_line() + 
geom_point() + 
scale_y_continuous(labels = scales::unit_format(scale = 1e-6)) +
ggtitle('ADSL Subscriptions') +
theme(plot.title = element_text(hjust = 0.5)) +
scale_color_viridis(discrete = TRUE)

ggplotly(g)
```

![png](i_sub_1.png)




```R
g <- ggplot(ict_stats, aes(x = Year, y = Mobile, color = Quarter)) + 
geom_line() + 
geom_point() + 
scale_y_continuous(labels = scales::unit_format(scale = 1e-6)) +
ggtitle('Mobile Phone Internet Subscriptions') +
theme(plot.title = element_text(hjust = 0.5)) +
scale_color_viridis(discrete = TRUE)

ggplotly(g)
```

![png](i_sub_2.png)



```R
library(scales)
library(gganimate)
colors <- viridis(8, option = 'A')
#show_col(colors)

```


```R
g <- ict_stats %>%
filter( Quarter == 'Q4') %>%
ggplot(aes(x = Year)) +
geom_line(aes(y = ADSL, colour='ADSL')) +
geom_line(aes(y = Mobile, colour='Mobile')) +
scale_y_continuous(labels = scales::unit_format(scale = 1e-6)) +
scale_color_manual(values = c(colors[3],colors[5]), name = 'Type') +
ggtitle('Number of Internet Subscribers') +
ylab('Subscribers') + 
theme(plot.title = element_text(hjust = 0.5))

ggplotly(g)
```

![png](i_sub_3.png)
