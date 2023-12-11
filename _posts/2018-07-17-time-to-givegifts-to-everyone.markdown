---
layout: post
title:  Predicting traffic in the New York City Subway
date:   2022-07-17 15:01:35 +0300
image:  nycSubwayMap.png
tags:   Urban planning
---
<small>This is joint work with Julieta Rivero and Rodrigo Villela.</small>

### Exploratory data analysis


![]({{ site.baseurl }}/images/mapa_calor_res.png)
*Heat map of the change in the use of the subway system after the pandemic.*

![]({{ site.baseurl }}/images/eda_zonas.png)
*Change in the use of the subway divided by zones in NYC.*

We can see that on average, the subway use got reduced the most in Manhattan. Queens has a lot of variance in the response variable, due to the fact that the whiskers in its box plot are very large. Whereas we see that the Bronx had low changes in the use of the subway with low variance.



### Prediction strategy
![]({{ site.baseurl }}/images/map_test_pred.png)
*Training the model and prediction strategy. We identified that Queens Village's change in the use of the subway was an outlier observation.*


### Regression model





