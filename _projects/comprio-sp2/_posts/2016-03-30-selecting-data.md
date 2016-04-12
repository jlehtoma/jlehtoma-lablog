---
layout: post
title: "Selecting and pre-processing data"
date: "2016-03-30"
updated: "2016-04-12"
tags:
 - comprio-sp2
 - data
---

## Potential datasets

See [potential datasets for SP2](https://docs.google.com/spreadsheets/d/1niV9Oe8pavgskiq0ibMzPt6F_oJU3uTD3R2pY7RwyDU/edit?usp=sharing). For further details and literature reference, see [this catalog](https://docs.google.com/spreadsheets/d/1NblQP0IGxXDUOXgqhzp03acPUMc2XJ6u_vPgWHC8OMk/edit?usp=sharing). This page describes the rationale for selecting datasets for the project "Comparing spatial prioritization methods for biodiversity conservation and ecosystem services" (SP2) and the pre-processing steps needed to prepare the data for the analysis.

Sheet `table_1_work` in the planning [Google Sheet](https://docs.google.com/spreadsheets/d/1niV9Oe8pavgskiq0ibMzPt6F_oJU3uTD3R2pY7RwyDU/edit?usp=sharing) includes information on the 1) extent and 2) resolution of all the potential datasets. At later stage, all the data needs to be translated into the same extent and resolution (see also [this Trello card](https://trello.com/c/aNFSPfhi)).

----

|  **ID** | **Category** | **Dataset** | **Description** |
|  ------ | ------ | ------ | ------ |
|  1 | BD | [Farmland birds](#farmland-birds) | Farmland bird species richness |
|  2 | BD | European vertebrate species | In particular, we considered the entire European sub-continent plus Turkey and a total of 1149 species of terrestrial vertebrates. For each species, we developed species-specific expert-based distribution models (validated against field data) which we used to calculate species richness maps for mammals, breeding birds, amphibians, and reptiles. Considering |
|  3 | ES | Megafauna habitat | Habitat suitability for megafauna (7 species) |
|  4 | BD | [Agro biodiversity](#agro-biodiversity) | Species richness of farmland vertebrates and plants |
|  5 | ES | Climate regulation | Response of terrestrial carbon balance to land use change scenarios |
|  6 | ES | Erosion prevention | Protection of land cover against erosion in erosion prone areas |
|  7 | ES | Flood regulation | Water retention capacity (supply and demand) |
|  8 | ES | Heritage: agriculutural landscapes | Landscape characterization based on the three dimensions of cultural landscape |
|  9 | ES | Heritage: forest landscapes | Landscape characterization based on the three dimensions of cultural landscape |
|  10 | ES | Pollination visitation probability | Pollinator visitation probability (supply) and cropland dependency on pollinators (demand) |
|  11 | ES | Pollination flows | Unmanaged pollinators that live in suitable natural and semi-natural habitats provide pollination services especially to near croplands. Benefiting areas depend on pollination service flows from neighboring habitats, due to a segregation between cropland and habitat |
|  12 | ES | Tourism | Supply of assets for tourism supported by ecosystems |
|  13 | ES | Wild food provisioning | Species richness of wild edible plants, mushrooms and game (supply) and demand of wild food |
|  14 | ES | Wood production | High-resolution wood production maps for European forests (average 2000-2010) |

----

### Biodiversity features

#### 1. Farmland birds

+ Filter the species (N=168) based on the following criteria:
  + Year = 2000
  + Scenario = A1
+ Add [Snake make rules](https://github.com/VUEG/data-EG/blob/master/farmland_birds/Snakefile) and [scripts](https://github.com/VUEG/data-EG/tree/master/farmland_birds/scripts) for translating all the birds species data from AIG (ArcInfo Grids) to GeoTIFF using `gdal_translate`.
+ Check the extent of all translated rasters using [farmland_birds/scripts/check_extents.py](https://github.com/VUEG/data-EG/blob/master/farmland_birds/scripts/check_extents.py). **Result:** all extents match.

#### 2. European vertebrate species

+ Data use pending on Rome.

### Ecosystem service features

#### 3. Megafauna

+ Data on the species components that were used to construct the layer (birds and mammals) is available, but this is too coarse (50x50km). Also, these composite layers don't contain information per species.

+ **Conclusion:** Used as a ES feature.

#### 4. Agro biodiversity

+ As described in [Overmars et al. (2014)](http://dx.doi.org/10.1016/j.ecolind.2012.11.006), the indicator layer includes data on 132 species maps on 50x50km resolution with the following additional data and processing:

![Overmars-et-al-2014-fig-1](http://ars.els-cdn.com/content/image/1-s2.0-S1470160X1200386X-gr1.jpg)

+ See [card in Trello](https://trello.com/c/jgSndp4C).

+ **Conclusion:** Can't be used as biodiversity feature, unless theres access to the underlying species maps (which are pretty coarse as well). Used as an ES feature.

#### 5. Climate regulation

+ **Conclusion:** Used as an ES feature.

#### 6. Erosion prevention

+ **Conclusion:** Used as an ES feature.

#### 7. Flood regulation

+ **Conclusion:** Used as an ES feature.

#### 8. Heritage: agriculutural landscapes

+ **Conclusion:** Used as an ES feature.

#### 9. Heritage: forest landscapes

+ **Conclusion:** Used as an ES feature.

#### 10. Pollination visitation probability

+ Pollination flows more suitable, as it also (kind of) includes the demand for pollination.
+ **Conclusion:** Not used.

#### 11. Pollination flows

+ **Conclusion:** Used as an ES feature.

#### 12. Tourism

+ **Conclusion:** Used as an ES feature.

#### 13. Wild food provisioning

+ **Conclusion:** Used as an ES feature.

#### 14. Wood production

+ **Conclusion:** Average 2000-2010 used as an ES feature.
