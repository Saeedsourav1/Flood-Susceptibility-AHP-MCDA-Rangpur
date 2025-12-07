# **Flood Susceptibility Mapping in the Rangpur Division Using AHP and Google Earth Engine–Based Multi-Criteria GIS Analysis**

## **Overview**

This repository presents a complete workflow for generating a **Flood Susceptibility Map** for the Rangpur Division of Bangladesh using an **Analytical Hierarchy Process (AHP)**–based Multi-Criteria Decision Analysis (MCDA) approach.

The study integrates multi-source geospatial datasets, hydrological derivatives, land-use classifications, and climatic variables to quantify the spatial likelihood of flooding. The modelling framework is designed to be **transparent, reproducible, and scalable**, supporting scientific research, disaster risk reduction, and spatial planning.

---

## **Objectives**

* Integrate **terrain, hydrological, climatic, and land-use parameters** for flood susceptibility modelling.
* Compute **AHP-derived weights** for eight flood-conditioning factors.
* Generate a **continuous Flood Susceptibility Index (FSI)** and a **five-class susceptibility map**.
* Produce **area-based susceptibility statistics** to identify critical flood-prone zones.
* Support evidence-based **flood mitigation, preparedness, and infrastructure planning**.

---

## **Data Sources**

Eight conditioning factors were used in the modelling approach:

| No. | Factor                       | Source / Repository       | Notes                                          |
| --- | ---------------------------- | ------------------------- | ---------------------------------------------- |
| 1   | DEM                          | *gee-hydrology-toolkit*   | Base for terrain and hydrological derivatives. |
| 2   | Slope                        | *gee-hydrology-toolkit*   | Derived from DEM.                              |
| 3   | Flow Accumulation            | *gee-hydrology-toolkit*   | Indicates flow concentration.                  |
| 4   | TWI                          | *gee-hydrology-toolkit*   | Represents soil moisture potential.            |
| 5   | Distance to River            | *gee-hydrology-toolkit*   | Euclidean distance to rivers.                  |
| 6   | Precipitation                | CRU (processed in ArcMap) | Long-term monsoon rainfall.                    |
| 7   | Land Use / Land Cover (LULC) | *LULC-Rangpur-2023*       | 2023 LULC dataset produced by the author.      |
| 8   | Elevation-derived Indicators | *gee-hydrology-toolkit*   | Additional terrain metrics.                    |

### **Referenced Repositories**

* 🌐 LULC 2023 Dataset:
  [https://github.com/Saeedsourav1/LULC-Rangpur-2023](https://github.com/Saeedsourav1/LULC-Rangpur-2023)
* 🌐 Hydrology Toolkit:
  [https://github.com/Saeedsourav1/gee-hydrology-toolkit](https://github.com/Saeedsourav1/gee-hydrology-toolkit)

---

## **Methodology**

The workflow is divided into four primary phases.

---

### **1. Data Acquisition & Preprocessing**

* Hydrological conditioning of DEM
* Slope & flow accumulation generation
* TWI computation
* Distance-to-river raster derivation
* CRU precipitation extraction
* LULC generation via author’s repository
* Projection to **UTM 45N**
* Raster alignment and clipping

---

### **2. AHP Weight Determination**

AHP was used to derive weights for the eight factors.

Steps:

* Constructing a pairwise comparison matrix
* Normalizing the matrix
* Eigenvector-based weight computation
* Consistency ratio (CR) validation (**acceptable when CR < 0.10**)

Weight calculation formula:

![AHP Weight](https://latex.codecogs.com/svg.latex?w_i%20=%20%5Cfrac%7B%5Csum_%7Bj=1%7D%5En%20a_%7Bij%7D%27%7D%7Bn%7D)

---

### **3. Flood Susceptibility Modelling**

Flood Susceptibility Index (FSI) was computed using a Weighted Linear Combination (WLC):

![FSI](https://latex.codecogs.com/svg.latex?FSI%20=%20%5Csum_%7Bi=1%7D%5E8%20%28w_i%20%5Ccdot%20f_i%29)

Where:

* **FSI** = Flood Susceptibility Index
* ( w_i ) = Weight of factor *i*
* ( f_i ) = Standardized raster value

Outputs:

* Continuous susceptibility raster
* Five-class zonation map (Very Low → Very High)

---

## **Repository Structure**

```
flood-susceptibility-ahp/
│
├── Images/
│   ├── Distance_to_river.png
│   ├── Elevation.png
│   ├── Flow_accumulation.png
│   ├── LULC.png
│   ├── NDVI.png
│   ├── Precipitation.png
│   ├── Slope.png
│   ├── upazila_bar_chart.png
│   ├── upazila_heatmap.png
│   └── result.md
├── src/
│   ├── AHP..xlsx
│   └── consistency.ipynb
│
└── methodology.md 
│
└── README.md    
│
└── Results.md   

```

---

## **Results**

The analysis produces:

* Flood Susceptibility Index raster
* Five-class susceptibility zonation
* AHP weight matrix
* Area distribution statistics for each class

Applications include:

* Disaster risk management
* Flood zoning and land-use policy
* Infrastructure vulnerability assessment
* Hydrological and environmental research

---

## **Citation**

If you use this repository, please reference:

```
Saeed Sourav. (2023). LULC-Rangpur-2023. GitHub Repository.
https://github.com/Saeedsourav1/LULC-Rangpur-2023

Saeed Sourav. (2024). GEE Hydrology Toolkit. GitHub Repository.
https://github.com/Saeedsourav1/gee-hydrology-toolkit

Saeed Sourav. (2025). Flood Susceptibility Mapping in Rangpur Division Using AHP and Multi-Criteria GIS Analysis. GitHub Repository.
https://github.com/Saeedsourav1/flood-susceptibility-ahp
```

---

## **License**

This project is protected under **All Rights Reserved**.

Unauthorized copying, reproduction, distribution, or modification of datasets, maps, scripts, or documentation is strictly prohibited without explicit written permission from the author.

---

## **Contact**

**Saeed Sourav**
Civil Engineer • Researcher
📧 Email: *[saeedsourav2@gmail.com](mailto:saeedsourav2@gmail.com)*
🌐 GitHub: [https://github.com/Saeedsourav1](https://github.com/Saeedsourav1)

---

