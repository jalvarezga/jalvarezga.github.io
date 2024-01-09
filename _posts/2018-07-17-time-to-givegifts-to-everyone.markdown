---
layout: post
title:  Predicting traffic in the New York City Subway
date:   2022-07-17 15:01:35 +0300
image:  nycSubwayMap.png
tags:   Urban planning
---


<script
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
  type="text/javascript">
</script>



<span style="color: red"> This is joint work with Julieta Rivero and Rodrigo Villela.</span>


## Data analysis

![]({{ site.baseurl }}/images/nycSections.png)
*Map of NYC divided by neighborhoods in the city's boroughs excluding Staten Island.*




![]({{ site.baseurl }}/images/mapa_calor_res.png)
*Heat map of the change in the use of the subway system after the pandemic.*





![]({{ site.baseurl }}/images/eda_zonas.png)
*Change in the use of the subway divided by zones in NYC.*

We can see that on average, the subway use got reduced the most in Manhattan. Queens has a lot of variance in the response variable, due to the fact that the whiskers in its box plot are very large. Whereas we see that the Bronx had low changes in the use of the subway with low variance.




### Variables

- $$\textbf{born_nys}:$$ porcentaje de la población del barrio que nació en Nueva York. Toma valores numéricos entre $$0$$ y $$100$$. 

- $$\textbf{prc_car_free}$$: porcentaje viviendas en el vecindario que no cuentan con un automóvil. Toma valores numéricos entre $$0$$ y $$100$$.

 - $$\textbf{disabled_pop}$$: porcentaje de la población en el barrio que tiene alguna discapacidad. Toma valores numéricos entre $$0$$ y $$100$$. 

- $$\textbf{foreign_pop}$$: porcentaje de la población del barrio que es extranjera. Toma valores numéricos entre $0$ y $100$. 

- $$\textbf{homeownership_rate}$$: porcentaje de viviendas del vecindario habitadas por sus dueños. Toma valores numéricos entre $0$ y $100$. 

- $$\textbf{houses_children}$$: porcentaje de hogares en los que vive al menos una persona menor de 18 años. Toma valores numéricos entre $0$ y $100$. 

- $$\textbf{housing_units}$$: número de unidades habitacionales en el vecindario.

- $$\textbf{work_travel_time}$$: tiempo promedio en minutos que hace un residente del vecindario a su trabajo.

- $$\textbf{income}$$: ingreso promedio anual por vivienda ubicada en el barrio en dólares estadounidenses del 2020.

- $$\textbf{prc_asian}$$: porcentaje de población asiática en el vecindario. Toma valores numéricos entre $0$ y $100$. 

- $$ \textbf{prc_hispanic}$$: porcentaje de hispanos que viven en el barrio. Toma valores numéricos entre $0$ y $100$. 

- $$\textbf{prc_black}$$: porcentaje de afrodescendientes que viven en el barrio. Toma valores numéricos entre $0$ y $100$. 

- $$\textbf{prc_white}$$: porcentaje de caucásicos que viven en el barrio. Toma valores numéricos entre $0$ y $100$. 

- $$\textbf{population}$$: número de habitantes en el vecindario.

- $$\textbf{pop_65}$$: porcentaje de habitates mayores a 65 años de edad. Toma valores numéricos entre $0$ y $100$. 

- $$\textbf{pop_density}$$: densidad poblacional. Se obtuvo calculando el número de habitantes por milla cuadrada y dividiendo esa cantidad entre $1,000$. Por lo tanto, si se multiplica esta variable por mil, se obtiene el número de habitantes por milla cuadrada en el barrio.

- $$\textbf{poverty_rate}$$: porcentaje de personas que viven en condiciones de pobreza en el barrio. Toma valores numéricos entre $0$ y $100$. 

- $$\textbf{public_housing_prc}$$: porcentaje de viviendas del vecindario subsidiadas por el gobierno. Toma valores numéricos entre $0$ y $100$. 

- $$\textbf{houses_subway}$$: porcentaje de viviendas en el vecindario que tienen una estación de metro a una distancia menor a 12 millas. Toma valores numéricos entre $0$ y $100$. 

- $$\textbf{houses_park}$$: porcentaje de unidades residenciales en el barrio que tienen un parque a una distancia menor a 14 millas. Toma valores numéricos entre $0$ y $100$. 

- $$\textbf{crime_rate}$$: número de crímenes que resultaron en encarcelamiento por cada $1,000$ habitantes de 16 años de edad en adelante. No está expresado porcentualmente pero, por ejemplo, el valor más grande que tenemos en la base es de $23.5$. Al  multiplicarlo por $100,000$  y dividir entre $1,000$ obtenemos el número de encarcelamientos por cada $100,000$ personas de 16 años y mayores, que sería de  $2,350$, es decir, el $2.35\%$ de los habitantes mayores de 15 años en ese barrio fueron encarcelados por algún crimen durante el 2020. 


- $$\textbf{unemployent_rate}$$: tasa de desempleo de los habitantes pertenecientes a la población económicamente activa de ese barrio. 

- $$\textbf{income_cat}$$: una versión categórica de la variable \textbf{\textit{income}}. Se divide en cuatro factores: \textit{bajo, medio, medio\_alto} y  \textit{alto}. Para elegir los puntos de corte que definen a las clases se usaron el primer cuartil US $\$49460$ , la mediana US $\$57680$  y el tercer cuartil US $\$71920$.

- $$\textbf{zones}$$: variable categórica que clasifica a los vacindarios según su ubicación en los siguientes distritos: \textit{Bronx, Brooklyn, Manhattan} y \textit{Queens}. 





## Prediction strategy

We randomly selected 15% of the neighborhoods and kept them to test the model. We trained the model with the 85% of the remaining neighborhoods.

![]({{ site.baseurl }}/images/map_test_pred.png)
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

$$\mathbf{\beta}$$ is the vector of unknown coefficientsd; additionallyn we assume that the explanatory variables are knon constants for each $$i$$.
On the other hand, the least squares estimator of $$\mathbf{\beta}$$ for the multiple regression model has the form

$$\begin{equation}\mathbf{\hat{\beta}}=(X'X)^{-1}X'\textbf{Y},\end{equation}$$

where $$X$$ is the design matrix and $$\textbf{Y}$$ es el vector que contiene a la muestra de la variable repuesta. Como podemos notar, la existencia de este estimador requiere que la matriz $X'X$ tenga inversa. Para garantizar invertibilidad, es necesario que la matriz de diseño, $X$, tenga rango completo, es decir, que sus columnas sean linealmente independientes. Por ejemplo, si una variable tiene muy poca varianza relativa a la magnitud de la variable, entonces es posible que su correspondiente columna en la matriz de diseño resulte linealmente dependiente de la primera columna de X, en cuyo caso el estimador de mínimos cuadrados no estaría definido. Otro posible problema sería que dos variables estén fuertemente correlacionadas entre sí, digamos, con correlación en valor absoluto mayor a $0.8$, lo cual daría lugar a inestabilidad en las operaciones numéricas para invertir $X'X$, debido a que $X$ tendría dos columnas (casi) linealmente dependientes. \\ 

Es por esta razón que es fundamental hacer un análisis exploratorio de las variables que se utlizarán para consturir el modelo de regresión lineal múltiple. Lo cual motiva la necesidad de familiarizarnos con las variables explicativas que usaremos, para así detectar este tipo de problemas y poder comprender a mayor profundidad su naturaleza de manera previa al modelaje. 




Finalmente, consideramos pertinente aclarar que en la siguiente sección se hacen algunos comentarios sobre las posibles razones detrás de la relación entre la variable de respuesta y las variables explicativas analizadas. Queremos recalcar que correlación no implica causalidad, y por lo mismo las ideas presentadas a continuación no deben de tomarse como afirmaciones de hechos causales, sino como posibles interpretaciones basadas en nuestro propio criterio de análisis. 








