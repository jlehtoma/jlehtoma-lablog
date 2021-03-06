---
layout: post
title: "Harmonizing data"
date: "2016-05-10"
updated: "2016-06-06"
tags:
 - priocomp-sp2
 - data
---

# 1. Ecosystem service features

## 1.1 Data harmonization

1. All [datasets used](../../../2016/03/30/selecting-data) - except European vertebrate species data and farmlands birds data - are downloaded from BeeHub by the [Snakemake rules](https://github.com/VUEG/priocomp/blob/master/Snakefile) in the [priocomp project](https://github.com/VUEG/priocomp).
2. Following data download, all datasets are warped/translated into the same SRS and projection. The reference raster used is `/data/external/datadryad/forest_production_europe/woodprod_average.tif`. This file is used because it a suitable geographical extent (~EU28) and the correct SRS (EPSG:3035, ETRS-LAEA).
3. What still remains to be done is to check to contextual coverage of different datasets, i.e. which regions/countries actually have data in them.

## 1.2 Data coverage

While all datasets have been harmonized in section 1., they may still contain data from different regions (point 3 in section1). To see which datasets cover which countries, rule [`build_data_coverage`](https://github.com/VUEG/priocomp/blob/master/Snakefile#L114) is used to construct a raster in which the value of each cell gives the count of how many datasets have data in that cell. Results look like this:

![data_coverage](https://raw.githubusercontent.com/VUEG/priocomp/master/reports/figures/data_coverage.png)

Eurostat countries without Croatia, Cyprus, Iceland, Macedonia, Malta, Montenegro. Norway, Switzerland, and Turkey are fairly well covered.

**Conclusion:** Use eurostat countries without the afore mentioned countries.

# 2. Biodiversity features

## 2.1 Data harmonization

## 2.2 Data coverage

# 3. Data normalization/standardization

According to [here](http://www.dataminingblog.com/standardization-vs-normalization/), following definitions can be used:

"Two methods are usually well known for rescaling data. *Normalization*, which scales all numeric variables in the range [0,1]. One possible formula is given below:

$ x_{new} = \frac{x - x_{min}}{x_{max} - x_{min}} $

On the other hand, you can use *standardization* on your data set. It will then transform it to have zero mean and unit variance, for example using the equation below:

$ x_{new} = \frac{x - \mu}{\sigma} $

Both of these techniques have their drawbacks. If you have outliers in your data set, normalizing your data will certainly scale the "normal" data to a very small interval. And generally, most of data sets have outliers. When using standardization, your new data aren't bounded (unlike normalization)."

## 3.1 Potential alternatives

Robust alternatives, such as:

1. Subtract the median and divide by the IQR, or
2. Scale linearly so that the 5th and 95th percentiles meet some standard range.

## 3.2 Examples from the literature

+ [Schulp et al. 2014](http://dx.plos.org/10.1371/journal.pone.0109643) used "[...] a min-max normalisation to cover the range [0,1] with 0 indicating the lowest value for an ES. The EV maps were computed using a linear combination of explaining variables, and therefore we assumed linearity for the normalization."

## 3.3 Look at the data

### 3.3.1 Data (ES features) histograms before rescaling

![histo_before_rescaling](https://raw.githubusercontent.com/VUEG/priocomp/master/reports/figures/harmonized_rasters_histogram.png)

### 3.3.2 Implementation

+ Project module [`src/data_processing/python/rescale.py`](https://github.com/VUEG/priocomp/blob/master/src/data_processing/python/rescale.py) implements different functions for rescaling.
  + **NOTE**: due to some issues with float precision, writing numpy.ndarray on disk using rasterio, and subsequently reading it will produce some loss in precision. Not sure how sever the problem is. values seems to be similar at least up to 4 decimal places.
  + **NOTE**: values in rasters can also be negative, as with carbon sequestration. Therefore rescaling must be able to handle negative values.

### 3.3.3 Data histograms after rescaling

Using normalization.

![histo_after_rescaling](https://raw.githubusercontent.com/VUEG/priocomp/master/reports/figures/processed_rasters_histogram.png)
![boxplot_after_rescaling](https://raw.githubusercontent.com/VUEG/priocomp/master/reports/figures/processed_rasters_boxplot.png)
