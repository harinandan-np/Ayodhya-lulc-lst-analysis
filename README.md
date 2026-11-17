# Land Use/Land Cover Change and Land Surface Temperature in Ayodhya District (2005–2025)

A remote sensing study of how land use, vegetation and surface temperature changed in Ayodhya district, Uttar Pradesh, using Landsat imagery and Google Earth Engine. This repository holds the maps, result tables and method from my M.Sc. Environmental Studies dissertation (University of Delhi, 2026).

**Tools:** Google Earth Engine (JavaScript) · Landsat 5 TM and Landsat 8 OLI/TIRS · Random Forest classification · QGIS (cartography)

---

## Key findings

- **Built-up land grew from 63.58 km² to 253.05 km² (+298%) between 2005 and 2025**, nearly four times its original size.
- **Agricultural land fell by 228.81 km²** (1,516.36 to 1,287.55 km²) but remained the dominant land use.
- **The forest and vegetation class rose by 49.77 km²** (460.01 to 509.78 km²). This class includes scrub, orchards and plantations, not only dense forest.
- **Mean land surface temperature (LST) rose by 2.90 °C from 2015 to 2025** (39.66 to 42.56 °C). Both years use the same sensor, so this change is the more reliable one.
- **Mean LST of built-up land rose by 3.21 °C from 2015 to 2025** (38.78 to 41.99 °C).
- **Barren land was the hottest class in all three years and water the coolest.** In this pre-monsoon window, built-up land was cooler than agricultural land (harvested fields are bare soil).

## Study area

Ayodhya district lies in the flat alluvial plains of the Middle Ganga Plain in Uttar Pradesh, with the Saryu (Ghaghara) river crossing its north. It covers about 2,099 km².

<table>
  <tr>
    <td align="center"><img src="images/study_area_ayodhya.png" width="100%"><br><sub>Ayodhya district</sub></td>
    <td align="center"><img src="images/study_area_uttar_pradesh.png" width="100%"><br><sub>Uttar Pradesh</sub></td>
    <td align="center"><img src="images/study_area_india.png" width="100%"><br><sub>India</sub></td>
  </tr>
</table>

## Data and method

| Item | Detail |
|---|---|
| Satellite data | Landsat 5 TM (2005); Landsat 8 OLI/TIRS (2015, 2025). Collection 2 Level 2 surface reflectance and surface temperature, from the Google Earth Engine catalogue |
| Time window | 1 April to 31 May in each year (pre-monsoon, clearest skies and strongest thermal contrast) |
| Pre-processing | Scenes with more than 20% cloud cover excluded; cloud, shadow, snow, cirrus and saturated pixels masked with the QA bands; USGS scale factors applied; median composite clipped to the district |
| Land cover classification | Random Forest, 100 trees, 5 classes (water, built-up, agriculture, forest, barren). Training polygons digitised on the composites with Google Earth imagery as reference, at least 50 polygons per class per year |
| Accuracy assessment | Confusion matrix on independent validation samples (stratified random sampling), reporting overall accuracy and Kappa |
| NDVI | (NIR − Red) / (NIR + Red) from surface reflectance |
| LST | Landsat Collection 2 Level 2 surface temperature band, summarised per year and per land cover class with zonal statistics |
| Output | 30 m GeoTIFFs; final maps compiled in QGIS |

<p align="center"><img src="docs/methodology_flowchart.png" width="55%"><br><sub>Workflow</sub></p>

## Results

### Land use/land cover maps

<table>
  <tr>
    <td align="center"><img src="images/lulc_2005.png" width="100%"><br><sub>2005</sub></td>
    <td align="center"><img src="images/lulc_2015.png" width="100%"><br><sub>2015</sub></td>
    <td align="center"><img src="images/lulc_2025.png" width="100%"><br><sub>2025</sub></td>
  </tr>
</table>

| Year | Water (km²) | Built-up (km²) | Agriculture (km²) | Forest (km²) | Barren (km²) |
|---|---|---|---|---|---|
| 2005 | 26.72 | 63.58 | 1,516.36 | 460.01 | 32.67 |
| 2015 | 28.02 | 155.80 | 1,426.26 | 464.41 | 24.19 |
| 2025 | 22.59 | 253.05 | 1,287.55 | 509.78 | 26.51 |
| **Net change 2005–2025** | −4.13 | **+189.47** | **−228.81** | +49.77 | −6.16 |

### Classification accuracy

| Year | Sensor | Overall accuracy | Kappa |
|---|---|---|---|
| 2005 | Landsat 5 TM | 82.92% | 0.776 |
| 2015 | Landsat 8 OLI/TIRS | 88.6% | 0.843 |
| 2025 | Landsat 8 OLI/TIRS | 91.4% | 0.881 |

The 2005 map is less accurate than the other two years (see limitations below).

### Vegetation (NDVI)

<table>
  <tr>
    <td align="center"><img src="images/ndvi_2005.png" width="100%"><br><sub>2005</sub></td>
    <td align="center"><img src="images/ndvi_2015.png" width="100%"><br><sub>2015</sub></td>
    <td align="center"><img src="images/ndvi_2025.png" width="100%"><br><sub>2025</sub></td>
  </tr>
</table>

| Year | Min | Mean | Max | Std. dev. |
|---|---|---|---|---|
| 2005 | −0.17 | 0.21 | 0.62 | 0.06 |
| 2015 | −0.24 | 0.31 | 0.70 | 0.09 |
| 2025 | −0.20 | 0.29 | 0.75 | 0.07 |

Mean NDVI did not fall even though farmland shrank. In April–May most fields in Ayodhya have already been harvested and read as bare soil, while forest, orchards and plantations keep their canopy, so the gain in forest-class area outweighs the loss of cropland in this season.

### Land surface temperature (°C)

<table>
  <tr>
    <td align="center"><img src="images/lst_2005.png" width="100%"><br><sub>2005</sub></td>
    <td align="center"><img src="images/lst_2015.png" width="100%"><br><sub>2015</sub></td>
    <td align="center"><img src="images/lst_2025.png" width="100%"><br><sub>2025</sub></td>
  </tr>
</table>

| Year | Min | Mean | Max | Std. dev. |
|---|---|---|---|---|
| 2005 | 28.58 | 45.71 | 64.99 | 3.24 |
| 2015 | 27.31 | 39.66 | 58.54 | 2.61 |
| 2025 | 29.93 | 42.56 | 63.88 | 2.14 |

Mean LST by land cover class:

| Year | Water | Built-up | Agriculture | Forest | Barren |
|---|---|---|---|---|---|
| 2005 | 38.68 | 46.01 | 46.21 | 43.59 | 49.27 |
| 2015 | 35.31 | 38.78 | 40.38 | 38.33 | 41.86 |
| 2025 | 37.03 | 41.99 | 42.98 | 41.35 | 44.53 |

The spread of temperatures across the district narrowed from 3.24 °C (2005) to 2.14 °C (2025), which the dissertation reads as the thermal environment becoming more uniform as impervious surfaces replace mixed land cover.

## Limitations

- **Two different sensors.** 2005 uses Landsat 5 TM and the other years use Landsat 8, and the two can differ by 1 to 3 °C over the same surface. The drop in mean LST from 2005 to 2015 is therefore partly a sensor effect, and only the 2015 to 2025 change is a like-for-like comparison.
- **The 2005 land cover map is the weakest** (overall accuracy 82.92%, Kappa 0.776) because of Landsat 5 image quality, limited historical reference imagery, and the difficulty of separating built-up from barren land in an agricultural landscape. Changes measured against the 2005 baseline need careful interpretation.
- **One season per year.** Each year is a single April–May snapshot, so NDVI reflects harvested-field conditions, not the full crop cycle.
- **The forest class is broad.** It includes scrub, orchards and plantations, and part of its gain may come from Landsat 8 detecting vegetation better than Landsat 5.
- **Drivers are context, not tested.** The dissertation links built-up growth to road expansion, airport development and temple-related construction, but these links were not tested statistically.

## Repository contents

```
├── README.md
├── images/      Study area, land cover, NDVI and LST maps (2005, 2015, 2025)
├── results/     Result tables as CSV files (area, accuracy, NDVI, LST)
└── docs/        Methodology flowchart
```

## Status

The results, maps and tables above come from my completed dissertation. The original Earth Engine script was not saved, so I am rebuilding it from the documented method and will add it to this repository as a `scripts/` folder once it reproduces the results.

## Author

**Harinandan N.P** · M.Sc. Environmental Studies, University of Delhi
LinkedIn: [linkedin.com/in/harinandan4916](https://www.linkedin.com/in/harinandan4916)
