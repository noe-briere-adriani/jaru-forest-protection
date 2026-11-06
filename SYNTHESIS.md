# Does protection slow deforestation? One-page synthesis

**Case study: Jaru Biological Reserve (Rondônia, Brazil), 2017-2025**

## Question

Is forest loss lower inside a strictly protected area than in the unprotected land around it, and how robust is that contrast once the errors of the map are taken into account?

## Approach

- **Site.** Jaru Biological Reserve (IUCN category Ia, about 3,470 km²), compared with a 10 km ring around it from which all other protected areas were excluded.
- **Mapping.** Dry-season composites of Sentinel-2 (NDVI, NBR) and Sentinel-1 (VV, VH) for each year 2017-2025, classified in Google Earth Engine (Python API) with a random forest trained on high-confidence Hansen labels. A pixel counts as lost if it is forest in 2017 and stays non-forest until 2025; patches below 0.54 ha are removed. The two thresholds were fixed before the validation.
- **Validation.** 220 points drawn at random in 10 map-based strata, labelled blind from Sentinel-2 image chips by one analyst, then area and accuracy estimated with 95 % confidence intervals (Olofsson et al., 2014). Hansen was used for training and comparison, never as validation truth.
- **Inside versus outside.** Loss rate by distance to the reserve boundary, and a comparison at equal exposure to the deforestation front.

## Main results

- **Ring.** About 224 km² of forest lost between 2018 and 2025 (95 % CI 144 to 305), that is 10.2 % of the 2017 forest (6.8 to 13.6 %), or about 1.3 % per year on average.
- **Map quality in the ring.** 95 % of the mapped loss is confirmed (85 to 100 %), but the map finds only about 66 % of the true loss (46 to 86 %); overall accuracy is 97 %.
- **Reserve.** No loss was found among the 55 points sampled in its large stable stratum. The loss rate is very small (about 0.1 %; Hansen gives 0.05 %), but a sample of this size can only bound it: a conservative upper bound is about 6 % of its forest.
- **Boundary.** Loss is almost nil beyond 1 km inside the reserve and about 9 % beyond 1 km outside. The change is a ramp of roughly 1 km on each side of the line rather than a step.
- **Equal exposure.** Most of the reserve's forest is far from deforestation fronts. At equal distance to the front, it would be expected to lose about 17 to 20 times more than it did.

## What this does and does not show

The contrast is large and survives a simple control for exposure. It is an association for one site, not proof that protection caused it. Reserves tend to be created where forest is already less threatened, boundary positions are imprecise, and roads, slope, land tenure and enforcement were not controlled.

## Main limitations

One site chosen for its contrast; training labels inherit Hansen's errors; one analyst labelled the 220 points in about 30 minutes, without a repeat to measure consistency; thin strata (10 to 20 points) make some standard errors approximate; events smaller than 0.54 ha or lasting less than a year are not mapped; 2017-2018 have about four times fewer acquisition days than later years.

## Tools

Python, Google Earth Engine, Sentinel-1/2, random forest, stratified area estimation, rasterio, NumPy, pandas, scikit-learn, Matplotlib.

**Code and full report:** [github.com/noe-briere-adriani/jaru-forest-protection](https://github.com/noe-briere-adriani/jaru-forest-protection)
