---
layout: post
title:  Predicting traffic in the New York City Subway
date:   2022-07-17 15:01:35 +0300
image:  nycSubwayMap.png
tags:   Project
---


<script
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
  type="text/javascript">
</script>



<span style="color: red"> This is joint work with Julieta Rivero and Rodrigo Villela.</span>


## Data analysis

![]({{ site.baseurl }}/images/nyc_subway/nycSections.png)
*Map of NYC divided by neighborhoods in the city's boroughs excluding Staten Island.*




![]({{ site.baseurl }}/images/nyc_subway/mapa_calor_res.png)
*Heat map of the change in the use of the subway system after the pandemic.*




![]({{ site.baseurl }}/images/nyc_subway/work_travel_time.png)
*Average time to work (in minutes) for people in each neighborhood in relation to the response variable.*

We can clearly appreciate a negative linear relationship between the variables. A possible reason for this relationship might be that for people whose time to work is very close, they can easily substitute the metro for walking or bycicle, for example, given that their commute to work is likely very short.








![]({{ site.baseurl }}/images/nyc_subway/eda_zonas.png)
*Change in the use of the subway divided by zones in NYC.*

We can see that on average, the subway use got reduced the most in Manhattan. Queens has a lot of variance in the response variable, due to the fact that the whiskers in its box plot are very large. Whereas we see that the Bronx had low changes in the use of the subway with low variance.




### Variables
We take distict and neighborhood as synonyms throughout the desctiption of the feature variables (predictive variables).

- $$\textbf{born_nys}:$$ percentage of the population on the neighborhood who were born in NYC. By definitition,  this variable takes values in $$[0,100]$$. 

- $$\textbf{prc_car_free}$$: percentage of living places in the neighborhood that do not have a car.porcentaje viviendas en el vecindario que no cuentan con un automóvil. Takes values in $$[0,100]$$.

 - $$\textbf{disabled_pop}$$: percentage of the population in the distirct who have certain 
disability.

- $$\textbf{foreign_pop}$$: percentage of people in the neighborhood who are foregin.

- $$\textbf{homeownership_rate}$$: percentage of living places such that the owner of the place lives in it.

- $$\textbf{houses_children}$$: porcentage of houses in which there is at least one person younger than 18 years old.

- $$\textbf{housing_units}$$: number of housing units in the neighborhood.

- $$\textbf{work_travel_time}$$: average time (in minutes) to work for a person living in the neighborhood.


- $$\textbf{income}$$: average anual income for a peron in the district (reported in terms of 2020 us dollars).

- $$\textbf{prc_asian}$$: percentage of the population in the district who are asian.

- $$ \textbf{prc_hispanic}$$: percentage of hispanic people living in the neighborhood.

- $$\textbf{prc_black}$$: percentage of african-american people living in the district.

- $$\textbf{prc_white}$$: percentage of white people living in the district.

- $$\textbf{population}$$: number of people living in the district.

- $$\textbf{pop_65}$$: percentage of habitants in the district who are older than 65 years old.

- $$\textbf{pop_density}$$: Population density. We constructed this variable by computing the number of habitants in the district per square mile and dividing it by 1,000.

- $$\textbf{poverty_rate}$$:percentage of people in the neighborhood who live in poberty.


- $$\textbf{public_housing_prc}$$: percentage of living places which are subsidized by the NY government.


- $$\textbf{houses_subway}$$: percentage of living places in the neighborhood such that they have a metro station within 12 miles or less.

- $$\textbf{houses_park}$$: percentage of living units in the neighborhood that have a park 14 miles or closer.

- $$\textbf{crime_rate}$$: number of crimes which resulted in jail for every $$1,000$$ people 16 years old or older. As an example, the biggest value that we have in the dataset is 
23.5. Multiplying it by 100,000  and dividing it by 1000 we obtain the number of people who went to jail for every 100,000 people. In this exaple we get that  $$2,350$$ people of 16 years old or older went to jail for every $$100,000$$ persons in that age range. That is, $$2.35\%$$  of the habitants older than 15 years old went to jail for some crime during 2020.

- $$\textbf{unemployent_rate}$$: unemployment rate in the neighborhood.

- $$\textbf{income_cat}$$: this a categorical version of the variable $$\textbf{income}$$. It is divided into 4 categories according to income thresholds that we fixed. It is divided into: low, medium, medium-high, and high income. 
To choose the thresholds we used the quantiles of the income variable: the first quantile US $$\$49,460$$ ,  the median of $$\$57,680$$ usd and the third quantile of $$\$71,920$$usd.

- $$\textbf{zones}$$: Categorical variable dividinf the neighborhoods according to their location:
Bronx, Brooklyn, Manhattan and Queens. 





## Prediction strategy

We randomly selected 15% of the neighborhoods and kept them to test the model. We trained the model with the 85% of the remaining neighborhoods.

![]({{ site.baseurl }}/images/nyc_subway/map_test_pred.png)
*Green neighborhoods were used only for training. Yellow neighborhoods were not used for training and were used to test the performance of the model. We identified that Queens Village's change in the use of the subway was an outlier observation.*


## Regression model

We implemented a classic regression model of the following form:

$$Y_i=\beta_0+\beta_{1}X_{1i}+\dots\beta_{p-1}X_{p-1,i}+\epsilon_{i}\quad,$$



where we suppose that 

$$\begin{equation}\epsilon_{i}\sim N(0,\sigma^2),\quad \forall i\in \{1,\dots n\}\end{equation}$$


$$\begin{equation}Cov(\epsilon_{i},\epsilon_{j})=0 \quad \forall i,j\in \{1,\dots n\} , i\neq j\end{equation}$$

$$\begin{equation}\mathbf{\beta}:=\begin{bmatrix}
           \beta_{0} \\
           \beta_{1} \\
           \vdots \\
           \beta_{p-1}
         \end{bmatrix},\end{equation}$$

$$\mathbf{\beta}$$ is the vector of unknown coefficients; additionally we assume that the explanatory variables are knon constants for each $$i$$.
On the other hand, the least squares estimator of $$\mathbf{\beta}$$ for the multiple regression model has the form

$$\begin{equation}\mathbf{\hat{\beta}}=(X'X)^{-1}X'\textbf{Y},\end{equation}$$

where $$X$$ is the design matrix and $$\textbf{Y}$$ is the vector containing the response variables.

Notice that the existence of such estimator requires that the matrix $$X'X$$ is invertible.







 Como podemos notar, la existencia de este estimador requiere que la matriz $X'X$ tenga inversa. Para garantizar invertibilidad, es necesario que la matriz de diseño, $X$, tenga rango completo, es decir, que sus columnas sean linealmente independientes. Por ejemplo, si una variable tiene muy poca varianza relativa a la magnitud de la variable, entonces es posible que su correspondiente columna en la matriz de diseño resulte linealmente dependiente de la primera columna de X, en cuyo caso el estimador de mínimos cuadrados no estaría definido. Otro posible problema sería que dos variables estén fuertemente correlacionadas entre sí, digamos, con correlación en valor absoluto mayor a $0.8$, lo cual daría lugar a inestabilidad en las operaciones numéricas para invertir $X'X$, debido a que $X$ tendría dos columnas (casi) linealmente dependientes. \\ 

Es por esta razón que es fundamental hacer un análisis exploratorio de las variables que se utlizarán para consturir el modelo de regresión lineal múltiple. Lo cual motiva la necesidad de familiarizarnos con las variables explicativas que usaremos, para así detectar este tipo de problemas y poder comprender a mayor profundidad su naturaleza de manera previa al modelaje. 




Finalmente, consideramos pertinente aclarar que en la siguiente sección se hacen algunos comentarios sobre las posibles razones detrás de la relación entre la variable de respuesta y las variables explicativas analizadas. Queremos recalcar que correlación no implica causalidad, y por lo mismo las ideas presentadas a continuación no deben de tomarse como afirmaciones de hechos causales, sino como posibles interpretaciones basadas en nuestro propio criterio de análisis. 








