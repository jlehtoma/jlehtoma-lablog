---
layout: post
title: "Method Implementation"
date: "2016-06-06"
tags:
 - priocomp-sp2
 - analysis
 - mehtods
---

# 1. Rarity-weighted richness

### 1.1 R implementation

Rarity-weighted richness was first explored together with other methods [using Zonation tutorial data](http://rpubs.com/jlehtoma/priocomp). For a very simple analyses, there was very little difference in terms of performance (i.e. amount of features covered by each rank priority range) among the different methods. I did the for exploration [initial implementation](https://github.com/VUEG/priocomp/blob/master/reports/exploratory/04_explore_prioritization.Rmd#L101) (line 101) in R. This was fast enough for exploration with the relatively small dataset included in the Zonation tutorial, but would probably be too slow for the European-scale data (4526x4410). Particularly ranking can be slow.  

### 1.2 Python implementation

For production use, I [implemented the RWR algorithm also in Python](https://github.com/VUEG/priocomp/blob/master/src/RWR/rwr.py#L22). This was a bit trickier than the R implementation because dealing with NoData and value summation requires explicit conversion between Numpy arrays and masked arrays. At the time of writing, there are no tests though. The implementation follows closely the R implementation with one significant difference: breaking ties in the ranking phase. In the R implementation, ties are broken randomly. In the Python implementation, ties are broken by giving the average values of the ranks to all tied values. This is perhaps not optimal, but at the time of writing [scipy.stats.mstats.rankdata](https://docs.scipy.org/doc/scipy-0.14.0/reference/generated/scipy.stats.mstats.rankdata.html) only has one strategy available for masked arrays ("average"). For regular arrays there would be more alternatives (though not "random"), but dealing with NoData with regular arrays would probably be pain.

Ranking can still be slow. For the European-scale data (4526x4410), the ranking procedure tool ~12 hours (OpenSUSE Tumbleweed 64bit, 12 GB RAM, Intel Core i5-5200U @ 2.20 GHz). The procedure has not been repeated, so it's unclear how consistent this timing is. Fortunately, the ranking does not depend on the number of features being analyzed.

# 2. Zonation

# 3. Gurobi MIP
