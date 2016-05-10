---
layout: post
title: "Harmonizing data"
date: "2016-05-10"
tags:
 - priocomp-sp2
 - data
---

## 1. Data harmonization


## 2. Data normalization/standardization

According to [here](http://www.dataminingblog.com/standardization-vs-normalization/), following definitions can be used:

"Two methods are usually well known for rescaling data. *Normalization*, which scales all numeric variables in the range [0,1]. One possible formula is given below:

$ x_{new} = \frac{x - x_{min}}{x_{max} - x_{min}} $

On the other hand, you can use *standardization* on your data set. It will then transform it to have zero mean and unit variance, for example using the equation below:

$ x_{new} = \frac{x - \mu}{\sigma} $

Both of these techniques have their drawbacks. If you have outliers in your data set, normalizing your data will certainly scale the "normal" data to a very small interval. And generally, most of data sets have outliers. When using standardization, your new data aren't bounded (unlike normalization)."

### Potential alternatives

Robust alternatives, such as:

1. Subtract the median and divide by the IQR, or
2. Scale linearly so that the 5th and 95th percentiles meet some standard range.
