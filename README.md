# Namma Metro Accessibility Analysis

A GIS-based analysis of population accessibility to Namma Metro stations using 5-, 10-, and 15-minute walking-network catchments.

**Author:** Sreeman Bondada  
**Institution:** Manipal Institute of Technology, Bengaluru, Karnataka

---

## Project Overview

This project evaluates the accessibility of Namma Metro stations in Bengaluru using Geographic Information Systems (GIS), walking-network analysis, and population data.

The primary objective is to determine how much population can realistically reach each metro station within different walking-time thresholds.

Instead of using simple circular buffers around metro stations, the project uses a pedestrian walking network to model accessibility areas. This provides a more realistic representation of how people can reach metro stations through available walking routes.

The analysis considers three walking-time thresholds:

- 5-minute walking accessibility
- 10-minute walking accessibility
- 15-minute walking accessibility

Population data is then integrated with these accessibility zones to estimate the population accessible within each time threshold.

The final dataset contains **81 Namma Metro station features**.

---

## Objectives

The major objectives of the project are:

1. Obtain and prepare Namma Metro station data.
2. Construct and prepare a pedestrian walking network for Bengaluru.
3. Project the spatial datasets into an appropriate metric coordinate reference system.
4. Generate walking-network accessibility zones for 5, 10, and 15 minutes.
5. Integrate population data with the accessibility zones.
6. Calculate population accessible within each walking-time threshold.
7. Calculate additional population gained between accessibility thresholds.
8. Classify metro stations according to their final accessibility characteristics.
9. Visualize the results using GIS maps and statistical plots.
10. Provide a reproducible GIS workflow for metro accessibility analysis.

---

## Methodology

The overall workflow followed in this project is:

```text
Metro Station Data
        |
        v
Coordinate System Preparation
        |
        v
Walking Network Preparation
        |
        v
5 / 10 / 15 Minute Walking Catchments
        |
        v
Population Data Integration
        |
        v
Population Accessibility Calculation
        |
        v
Population Gain Analysis
        |
        v
Accessibility Classification
        |
        v
Final Visualization and Results