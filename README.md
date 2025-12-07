# **Flood Susceptibility Mapping in Rangpur Division Using AHP and Multi-Criteria GIS Analysis**

## **Overview**

This repository presents a complete workflow for generating a **Flood Susceptibility Map** for the Rangpur region of Bangladesh using an **Analytical Hierarchy Process (AHP)**–based Multi-Criteria Decision Analysis (MCDA) approach.
The project integrates multi-source geospatial datasets, hydrological derivatives, land use information, and climatic variables to characterize the spatial likelihood of flood occurrence.

The modelling framework ensures a **transparent, accurate**, and **scalable** methodology suitable for scientific research, disaster risk reduction, and spatial planning.

---

## **Objectives**

* To integrate **terrain, hydrological, climatic, and land-use factors** for flood susceptibility modelling.
* To compute **AHP-derived weights** for eight flood-conditioning parameters.
* To generate a **continuous flood susceptibility index** and a **5-class zonation map**.
* To deliver **area-wise flood susceptibility statistics** to identify zones of Very Low to Very High vulnerability within the study area.
* To support informed decision-making for **flood mitigation, preparedness, and infrastructure planning**.

---

## **Data Sources**

Eight conditioning factors were used for flood susceptibility modelling:

| No. | Feature                         | Source Repository / Dataset           | Notes                                                   |
| --- | ------------------------------- | ------------------------------------- | ------------------------------------------------------- |
| 1   | DEM                             | *gee-hydrology-toolkit*               | Base for terrain and hydrological derivatives.          |
| 2   | Slope                           | *gee-hydrology-toolkit*               | Derived from DEM.                                       |
| 3   | Flow Accumulation               | *gee-hydrology-toolkit*               | Indicates runoff concentration.                         |
| 4   | TWI (Topographic Wetness Index) | *gee-hydrology-toolkit*               | Represents soil moisture accumulation potential.        |
| 5   | Distance to River               | *gee-hydrology-toolkit*               | Euclidean distance from major drainage networks.        |
| 6   | Precipitation                   | CRU Time-Series (processed in ArcMap) | Long-term monsoon rainfall indicator.                   |
| 7   | Land Use / Land Cover (LULC)    | *LULC-Rangpur-2023*                   | Independent 2023 LULC dataset created by the author.    |
| 8   | Elevation-derived indicators    | *gee-hydrology-toolkit*               | Secondary terrain parameters supporting AHP evaluation. |

**Referenced GitHub Repositories:**

* 🌐 LULC 2023: [https://github.com/Saeedsourav1/LULC-Rangpur-2023](https://github.com/Saeedsourav1/LULC-Rangpur-2023)
* 🌐 Hydrological Toolkit: [https://github.com/Saeedsourav1/gee-hydrology-toolkit](https://github.com/Saeedsourav1/gee-hydrology-toolkit)

---

## **Methodology**

The workflow follows four major phases:

### **1. Data Acquisition & Preprocessing**

* DEM hydrological correction
* Slope and flow accumulation generation
* TWI computation
* Distance-to-river raster generation
* CRU precipitation processing in ArcMap
* LULC extraction from the author’s LULC repository
* Projection to UTM Zone 45N and raster alignment
* Study area clipping

All preprocessing steps are stored in `/scripts/01_extract_features`.

---

### **2. AHP Weight Determination**

AHP was used to determine the relative contribution of each conditioning factor.

Steps:

* Pairwise comparison matrix generation
* Computation of normalized eigenvector weights
* Consistency Ratio (CR) validation (acceptable when CR < 0.1)
* Exporting final AHP weights

Files are stored in `/docs/methodology.md`.

---

### **3. Flood Susceptibility Modelling**

A weighted linear combination (WLC) approach was applied:

[
FSI = \sum_{i=1}^{8} (w_i \cdot f_i)
]

Where:

* **FSI** = Flood Susceptibility Index
* **( w_i )** = AHP weight of factor *i*
* **( f_i )** = Standardized raster of factor *i*

Outputs include:

* Continuous susceptibility index raster
* Five-class hazard map (“Very Low” → “Very High”)

Scripts are inside `/docs/weighted_calculattion`.

---

## **Repository Structure**

```
flood-susceptibility-ahp/
│
├── results/
│   ├── Distance to river.png
│   ├── Elevation.png
│   ├── Flow accumulation.png
│   ├── LULC.png
│   ├── NDVI.png
│   ├── Precipitation.png
│   ├── slope.png
│   ├── upazilla bar chart.png
│   ├── upazilla heatmap.png
└── result.md



└── docs/
    ├── AHP.xlsx
    └── methodology.md
```

---

## **Results**

* Flood Susceptibility Index (FSI) raster
* 5-class zonation map (Very Low → Very High)
* AHP weight table
* **Area distribution by susceptibility class**, identifying which parts of the study area are more vulnerable

These results support:

* Disaster management & emergency planning
* Flood zoning & land-use regulation
* Infrastructure risk assessment
* Hydrological and environmental research

---

## **Citation**

If you use this repository, please cite:

```
Saeed Sourav. (2023). LULC-Rangpur-2023. GitHub Repository.
https://github.com/Saeedsourav1/LULC-Rangpur-2023

Saeed Sourav. (2024). GEE Hydrology Toolkit. GitHub Repository.
https://github.com/Saeedsourav1/gee-hydrology-toolkit

Saeed Sourav. (2025). Flood Susceptibility Mapping in Rangpur Division Using AHP and Multi-Criteria GIS Analysis. GitHub Repository.
https://github.com/Saeedsourav1/LULC-Rangpur-2023
```

---


## **License**

This project is protected under **All Rights Reserved**.

No part of the datasets, maps, scripts, figures, or documentation in this repository may be copied, reproduced, modified, distributed, or used for any purpose without explicit written permission from the author.

Unauthorized use is strictly prohibited.

---


## **Contact**

**Saeed Sourav**
Civil Engineer | Researcher
Email: [saeedsourav2@gmail.com](mailto:saeedsourav2@gmail.com)
GitHub: [https://github.com/Saeedsourav1](https://github.com/Saeedsourav1)

---

