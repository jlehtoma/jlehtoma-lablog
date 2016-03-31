---
layout: post
title: "IUCN data layers from CBIG"
date: "2016-03-31"
tags:
 - cbig
 - data
---

+ Peter Kullberg sent over a set of IUCN species layers used in Pouzols et al. (2014) at resolution `r19` (~10 km at the equator).
+ Use `unzip -l XX.zip | grep '\.tif$' | wc -l` to count the number of individual species rasters in each archive:
  + `IUCN_AmphibiansCBIGClassification_r19o.zip`: 6265
  + `IUCN_BirdsCBIGClassification_r19o.zip`: 10 073
  + `IUCN_MammalsCBIGClassification_r19o.zip`: 5412
  + `IUCN_ReptilesCBIGClassification_r19o.zip`: 3086
  + **Total: 24 836**
