# Namma Metro Accessibility Analysis

A GIS-based analysis of population accessibility to Namma Metro stations using 5-, 10-, and 15-minute walking-network catchments.

**Author:** Sreeman Bondada  
**Institution:** Manipal Institute of Technology, Bengaluru, Karnataka

---

## Project Overview

This project uses Geographic Information Systems (GIS) to evaluate how much population can practically access Namma Metro stations within different walking-time thresholds.

Instead of relying only on circular distance buffers, the project uses a walking network to construct accessibility areas around metro stations. Population data are then summarized within these accessibility areas using zonal statistics.

The analysis compares:

- 5-minute walking accessibility
- 10-minute walking accessibility
- 15-minute walking accessibility
- Population gain from 5 to 10 minutes
- Population gain from 10 to 15 minutes
- Population gain from 5 to 15 minutes
- Final accessibility classification

The final integrated dataset contains **81 metro station features**.

### Final Accessibility Classification

| Class | Stations | Share |
|---|---:|---:|
| High | 18 | 22.2% |
| Moderate | 13 | 16.0% |
| Low | 50 | 61.7% |
| **Total** | **81** | **100%** |

---

## Objectives

1. Prepare and integrate Namma Metro station, population and walking-network datasets.
2. Use a projected coordinate reference system suitable for distance-based GIS analysis.
3. Generate 5-, 10- and 15-minute walking accessibility areas.
4. Estimate population accessible within each threshold.
5. Calculate incremental population gain between accessibility thresholds.
6. Classify stations into High, Moderate and Low accessibility categories.
7. Visualize the results using QGIS maps and DataPlotly charts.
8. Produce a reproducible GIS workflow that can be extended to future metro accessibility studies.

---

## Study Area

The study focuses on Bengaluru, Karnataka, India, and the Namma Metro station network represented in the project datasets.

The spatial workflow uses:

**EPSG:32643 — WGS 84 / UTM zone 43N**

This is a projected CRS with metre-based units, making it appropriate for network-distance and spatial analysis operations.

---

## Data Used

### 1. Metro Stations

**Layer:** `metro_stations_utm43`

- Format: GeoPackage
- Geometry: Metro station features
- CRS: EPSG:32643
- Feature count: 81

### 2. Walking Network

**Layer:** `walking_network_utm43`

- Format: GeoPackage
- Geometry: LineString
- CRS: EPSG:32643
- Feature count: 238,269
- Approximate file size: 60 MB

The walking network provides the network structure used for accessibility analysis.

### 3. Population Raster

**Layer:** `bengaluru_population_2020_utm43`

- Format: GeoTIFF
- Data type: Float32
- Dimensions: 891 × 681
- Approximate pixel size: 91.10 m × 91.10 m
- CRS: EPSG:32643
- Population dataset representing 2020 conditions

---

## Methodology

The project follows the workflow below:

```text
Metro Station Data
        │
        ▼
Coordinate System Preparation
        │
        ▼
Walking Network
        │
        ▼
5 / 10 / 15 Minute Network Catchments
        │
        ▼
Population Raster
        │
        ▼
Zonal Statistics
        │
        ▼
Population by Station
        │
        ▼
Population Gain Calculations
        │
        ▼
Accessibility Classification
        │
        ▼
Maps + Charts + Master Dataset
```

### Step 1 — Spatial Data Preparation

Metro station data, population data and the walking network were prepared in a common projected coordinate system.

### Step 2 — Walking Accessibility

Network-based service areas were generated using 5-, 10- and 15-minute walking thresholds.

The network approach is important because actual walking accessibility depends on available paths rather than straight-line distance.

### Step 3 — Population Estimation

Zonal statistics were applied to the population raster using the accessibility areas as zones.

This produced station-level population measures for the different walking thresholds.

### Step 4 — Population Gain

The following measures were derived:

```text
Population Gain (5–10)
= Population(10 min) − Population(5 min)

Population Gain (10–15)
= Population(15 min) − Population(10 min)

Population Gain (5–15)
= Population(15 min) − Population(5 min)
```

### Step 5 — Accessibility Classification

The final `access_class` field categorizes stations into:

- **High**
- **Moderate**
- **Low**

The classification was visualized in QGIS using green, yellow and red symbols respectively.

---

## Key Results

### Accessibility Distribution

The final dataset contains:

- **18 High-accessibility stations**
- **13 Moderate-accessibility stations**
- **50 Low-accessibility stations**

The Low category therefore represents the largest group in the final classification.

### Highest 5–15 Minute Population Gains

Among the highest values inspected in the final master dataset were:

| Rank | Station | Population Gain (5–15 min) |
|---:|---|---:|
| 1 | Vijayanagar | ~209,887 |
| 2 | Srirampura | ~207,569 |
| 3 | Rajajinagar | ~201,244 |
| 4 | Mahakavi Kuvempu | ~200,043 |
| 5 | Sri Balagangadharanatha Swamiji Station | ~195,679 |
| 6 | Krishna Rajendra Market | ~190,155 |
| 7 | Chickpete | ~189,533 |
| 8 | Mahalakshmi | ~188,557 |
| 9 | Attiguppe | ~188,428 |
| 10 | Magadi Road | ~172,162 |

These values show where extending the walking threshold from 5 to 15 minutes reaches substantially more population.

---

## Interpretation

The analysis demonstrates that accessibility changes considerably with walking time.

A 5-minute catchment represents the immediate station service area. Increasing the threshold to 10 and then 15 minutes allows the network catchment to reach additional neighborhoods and population.

The population-gain metric is particularly useful because it identifies stations where extending the practical walking catchment produces the greatest additional population reach.

However, population accessibility should not be interpreted as actual metro ridership. Ridership is also affected by employment, schools, commercial activity, interchange behavior, feeder services, travel demand and other socioeconomic factors.

---

## Visualization

The project includes:

- Final QGIS accessibility map
- Accessibility-class distribution chart
- Population-gain bar chart
- 15-minute population-accessibility chart

The final map uses:

- 🟢 High
- 🟡 Moderate
- 🔴 Low

---

## Technologies Used

- **QGIS** — GIS processing, spatial analysis and cartography
- **DataPlotly** — statistical visualization
- **GeoPackage (GPKG)** — vector spatial data storage
- **GeoTIFF** — population raster storage
- **CSV** — final tabular data export
- **Network analysis** — walking accessibility
- **Zonal statistics** — population estimation

---

## Project Structure

```text
NammaMetroAccess/
│
├── README.md
├── NammaMetroAccess.qgz
│
├── data/
│   ├── raw/
│   └── processed/
│
├── output/
│
├── qgis/
│
├── quick_map_services/
│
├── scripts/
│
├── reports/
│   └── Namma_Metro_Accessibility_Detailed_Project_Report_Sreeman_Bondada.docx
│
└── Namma_Metro_Accessibility_Map.png
```

Some large spatial datasets may be managed separately using Git LFS or excluded from normal Git tracking depending on their size and redistribution requirements.

---

## Limitations

1. The population raster represents 2020 conditions and may not reflect current population distribution.
2. The raster has an approximate 91 m spatial resolution, which generalizes fine-scale population variation.
3. Accessibility results depend on the completeness and accuracy of the walking network.
4. Walking-time analysis depends on assumptions regarding walking speed and network traversal.
5. The High/Moderate/Low classification is specific to this project and is not an official Namma Metro rating.
6. Population accessibility does not directly represent actual metro ridership.
7. Barriers, pedestrian crossings, station entrances and local pedestrian conditions may not be completely represented.

---

## Future Work

Possible extensions include:

- Updating the population dataset with more recent estimates.
- Incorporating detailed pedestrian crossings and station entrances.
- Comparing accessibility with actual metro ridership.
- Adding employment and land-use data.
- Performing demographic accessibility analysis.
- Evaluating proposed future metro extensions.
- Building a combined accessibility index using population, employment and transport connectivity.

---

## Reproducibility

The QGIS project and supporting datasets can be used to reproduce the spatial workflow.

For a reproducible setup:

1. Open the QGIS project.
2. Verify that all data sources resolve correctly.
3. Confirm the project CRS is EPSG:32643.
4. Verify the station and walking-network layers.
5. Verify the population raster.
6. Re-run the accessibility and zonal-statistics workflow if necessary.
7. Recalculate population-gain fields.
8. Recreate the final classification and visualizations.

---

## Project Status

| Component | Status |
|---|---|
| Metro station data | Completed |
| Walking network | Completed |
| Population raster preparation | Completed |
| 5-minute accessibility | Completed |
| 10-minute accessibility | Completed |
| 15-minute accessibility | Completed |
| Population zonal statistics | Completed |
| Population-gain analysis | Completed |
| Accessibility classification | Completed |
| 81-station master dataset | Completed |
| DataPlotly visualizations | Completed |
| Detailed project report | Completed |
| Final map presentation | Completed |
| GitHub repository | In progress |

---

## Author

**Sreeman Bondada**  
**Manipal Institute of Technology**  
**Bengaluru, Karnataka, India**

---

## Academic Note

This project was developed as an applied GIS and urban transportation accessibility study. It demonstrates the integration of spatial network analysis, raster population analysis, zonal statistics, attribute engineering and cartographic visualization to study public-transport accessibility.
