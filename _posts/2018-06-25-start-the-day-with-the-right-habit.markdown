---
layout: post
title:  Predicting crimes in Boston
date:   2023-06-25 15:01:35 +0300
image:  todd-kent-Boston-unsplash.jpg
tags:   Urban planning
---



<small>Boston, Massachusetts. Photo by courtesy of  [Todd Kent](https://unsplash.com/@churchoftodd).</small>



This is joint work with Diego Velazquez and Marcelino Sanchez.

<script
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
  type="text/javascript">
</script>


[comment]: <> (Necessaty code to add LaTeX notation in this environment)





<small><span style="color: red"> Disclaimer: though fancy and useful, this kind of bayesian predictive algorithm is highly discouraged in high-risk scenarios, since it does not provide any theoretical guarantee on the coverage. One may take the point predictions made by the bayesian model and conformalize them to get rigorous coverage guarantees.</span></small>

### Context

The government of the City of Boston runs a very modern approach focused on a data culture to monitor and improve the quality of life in the city and it has available [open data](https://data.boston.gov/) website which offers gathered infomration by Boston's Police Department about crimes happening in the city. Anlayze Boston also reports census data for Boston's districts, containg detailed information about Boston's depographic characteristics.  Among other things, this site offers information about the kind of crime, location and time in which the crime happened.


![]({{ site.baseurl }}/images/boston/cover.png)
*A map of Boston's streets.*

We created spatial regression models with a bayesian approach to determine the predictive capacity of demographic variables to determine crime rates for each of Boston's districts. 

### Variables

We used the data base of the crimes that occured during 2022 in the City of Boston reported by the Boston Police Department.
This data base not only includes crimes but many other kind of activities that are reported to the police such as suicides, use of drugs, etc. We restricted the data to observations that were interpretable kinds of crime such as murder, shooting, larceny, shoplifting, valdalism,  etc. We only used the observations that we consider would help us get an insight about tghe crime situation in Boston. We constructed the response variable following the procedure that we present next.

We had two datasets: the crimes in 2022 and demographic charactersitics of the 22 districts in Boston collected in the census. Both datasets are availale in [Analyze Boston](https://data.boston.gov/). The crimese datset contains the location of the crime (in coordinates), district in which the crime occured, type of crime, time at which it was reported to the police, among others. We assigned a centroid to each of the city's district, by selecting a point that we considered to be central within the district.  We then assigned a label to each crime determined by the closest centroid. Finally, we counted how many crimes we had per district and divided them by the population size acccording to the census 

In notation, if i ∈ {1, . . . , 22} is the i-th district in Boston and there occured 
$$Z_i$$ ∈ $$\mathbb{N}$$ crimes in 2022 and according to the census of 2019, there were 
$$M_i$$ ∈ $$\mathbb{N}$$  people in the i-th district, then we took $$Y_i := \frac{Z_i}{M_i}$$ ∈ (0, ∞).
$$Y_i$$ tells us the crime rate in district $$i$$: the number of crimes per capita in 2022 realtive to 2019's population. 
Actually, given the nature of the data, and as we would expect to have more people than crimes in each neighborhood, then  
 $$Y_i$$ ∈ (0, 1) ∀i ∈ {1, . . . , 22}. In order to adjust the model and work in all $$\mathbb{R}$$, we consider an invertible transformation 



 $$\begin{equation}Y (s_i) := log(Y_i),\end{equation}$$

 where   $$s_i$$ ∈ $$\mathbb{R}^2$$ are the coordinates of the i-th district (the centroid).
 
 
 Hence, we consider our response variable as crime rates at a logarithmic scale. 


With respect to the feature variables, the 2019 census of Boston offers a lot of details about each district. For example, distance to the closest park for each home within each district, average anual income in usd, average time to work, proportion of houses that own a car, etc.




### Data analysis



![]({{ site.baseurl }}/images/boston/density.png)
*Distribution of crimes per day in Boston during 2022.*


![]({{ site.baseurl }}/images/boston/backBay.png)
*Crimes in the Back Bay area by the location in which they occured.*




![]({{ site.baseurl }}/images/boston/bostonMap.png)
*A map of Boston divided by neighborhoods.*


![]({{ site.baseurl }}/images/boston/crimePoints.png)
*Red points are district centroids. Light blue points are locations where a crime occured.*

![]({{ site.baseurl }}/images/boston/crimesByDistrict.png)
*A satellite image of Boston whith crime points stratified by neighborhood. The points are spread throughout almost all of the city.*



# Model proposal: a Gaussian process
We are going to consider point referenced data using a Gaussian process to incorporate a spatial dependence structure within the data. If 
$$s_i\in \mathbb{R}^2$$ denotes the coordinates of the $$i-th$$ district in Boston, the regresion model that we will be using is given by:

 
$$\begin{equation}Y(s)=\mathbf{\mu}(s)+\mathbf{\omega}(s)+\mathbf{\epsilon}(s),\end{equation}$$
with


$$\begin{equation}Y(s):=\begin{pmatrix}Y(s_1)\\Y(s_2)\\
\vdots\\
Y(s_n)
\end{pmatrix},\end{equation}$$

$$\begin{equation}\mathbf{\mu}(s):= \begin{pmatrix}\mu(s_1)\\ \mu(s_2)\\
\vdots\\
\mu(s_n)
\end{pmatrix},
\end{equation}$$


$$\mu(s_i)=\mathbf{x}(s_i)^{T}\mathbf{\beta}, $$ 
where $$\mathbf{x}(s_i)$$ denotes a feature vector that contains the predictive variables for the variables associated to the i-th neighborhood and  $$\begin{equation}\mathbf{\beta}=\begin{pmatrix}
    \beta_1 \\
    \beta_2\\
    \vdots \\
    \beta_p \end{pmatrix}\end{equation}$$

is a vector of coefficicients.


$$\begin{equation}\mathbf{\omega}(s):=\begin{pmatrix}w(s_1)\\w(s_2)\\
\vdots\\
w(s_n)
\end{pmatrix} \sim N_{n}\Big(\mathbf{0} , \Sigma(s,t)\Big)\end{equation}$$

denotes a Gaussian process that corresponds to the spatial dependence structure in the data, usinga an exponential covariance function. That is, if $$s_i, s_j$$ are the coordinates of two arbitrary districts in Boston, then 

$$\begin{equation}Cov(w(s_i), w(s_j))=\Sigma(s_i,s_j)=\sigma^2exp\{ -\phi d_{i,j}\},\end{equation}$$

where $$d_{i,j}:= \| s_i-s_j\|_{2}$$ is the Euclidean distance between the coordinates of districts $$i$$ and $$j$$.

And

$$\mathbf{\epsilon}(s) :=\begin{pmatrix}\epsilon(s_1)\\ \epsilon(s_2)\\
\vdots\\
\epsilon(s_n)
\end{pmatrix} \sim N_{n}\Big(\mathbf{0}, \varphi^2 I_{n\times n} \Big)$$
denotes the errors which we assume to be independent of  $$\mathbf{\omega}(s)$$.



As a consequence of such specification, we get that

$$\begin{equation}Y(s)\sim N_{n}\Big(\mathbf{\mu}(s),\Sigma(s,t)+\varphi^2 I_{n\times n} \Big).\end{equation}$$



Notice that this is a linear regresion to the mean model, given that we propose a linear combination of the feature variables which affects the mean  of the response variable.
We propose models of such a structure, using different explanatory variables (features), using a Bayesian approach.

Moreover, the prior distribution of the parameters $$\phi, \varphi^2, \sigma^2$$ is given by a non-infomrative Gamma.  It is important to keep in mind that by default, BUGS uses precision in the parametrization of the normal distribution and not the variance. 
For implementation purposes, we ran 2 chains of longitude $$10,000$$ with a thining of 20 units and a burning period of $$1,000$$ iterations with OpenBUGS.





# Prediction analysis

![]({{ site.baseurl }}/images/boston/BayesianKriging.png)
*We used a bayesian kriging approach to make predictions. We randomly chose two districts maked in orange and kept them to make predictions unobserved during training. We used the rest of the neighborhoods to train the model.*


![]({{ site.baseurl }}/images/boston/compareHeatMaps.png)
*Comparison between the original crime rate heat map and the crime rate heat ma generated using the  Model 1.*

![]({{ site.baseurl }}/images/boston/intervals.png)
*Point and prediction intervals as a function of average anual income in Boston's neighborhoods.*



![]({{ site.baseurl }}/images/boston/intervalPredictions.png)
*Point and interval predictions for neighborhoods that we didn't use during training.*

