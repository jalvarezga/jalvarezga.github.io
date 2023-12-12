---
layout: post
title:  Predicting crimes in Boston
date:   2023-06-25 15:01:35 +0300
image:  todd-kent-Boston-unsplash.jpg
tags:   Urban planning
---
This is joint work with Diego Velazquez and Marcelino Sanchez.

<script
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
  type="text/javascript">
</script>
[comment]: <> (Necessaty code to add LaTeX notation in this environment)




<small><span style="color: red"> Disclaimer: though fancy and useful, this kind of bayesian predictive algorithm is highly discouraged in high-risk scenarios, since it does not provide any theoretical guarantee on the coverage.</span></small>


### Data analysis

![]({{ site.baseurl }}/images/cover.png)
*A map of Boston's streets.*



![]({{ site.baseurl }}/images/density.png)
*Distribution of crimes per day in Boston during 2022.*


![]({{ site.baseurl }}/images/backBay.png)
*Crimes in the Back Bay area by the location in which they occured.*




![]({{ site.baseurl }}/images/bostonMap.png)
*A map of Boston divided by neighborhoods.*


![]({{ site.baseurl }}/images/crimePoints.png)
*Red points are district centroids. Light blue points are locations where a crime occured.*

![]({{ site.baseurl }}/images/crimesByDistrict.png)
*A satellite image of Boston whith crime points stratified by neighborhood. The points are spread throughout almost all of the city.*



#Model proposal: a Gaussian process


