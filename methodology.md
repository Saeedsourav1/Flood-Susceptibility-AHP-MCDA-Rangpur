# **📄 Methodology for Flood Susceptibility Mapping Using AHP and Multi-Criteria GIS Analysis**

## **1. Introduction**

Flood susceptibility mapping aims to quantify the spatial likelihood of flooding based on terrain, hydrological, climatic, and land-use characteristics. This study employs the **Analytical Hierarchy Process (AHP)** integrated with GIS-based multi-criteria analysis to assess flood-prone zones within the Rangpur region of Bangladesh.

AHP provides a structured framework to determine the relative significance of multiple flood-conditioning factors based on expert knowledge, hydrological theory, and empirical evidence. GIS then spatially applies these weights to generate a Flood Susceptibility Index (FSI).

---

# **2. Overall Workflow**

The methodological framework consists of the following stages:

1. **Data Collection**
2. **Raster Preprocessing & Hydrological Derivation**
3. **Standardization of Conditioning Factors**
4. **AHP Weight Calculation**
5. **Weighted Linear Combination (WLC) Modelling**
6. **Flood Susceptibility Classification**
7. **Area-Based Susceptibility Assessment**

Each stage is described in depth below.

---

# **3. Data Collection & Description of Flood Conditioning Factors**

Eight conditioning factors were selected based on their relevance in influencing flood behavior in floodplain environments:

### **3.1 Digital Elevation Model (DEM)**

* Source: gee-hydrology-toolkit
* Role: Governs terrain slope, drainage direction, and accumulation.
* Lower elevation generally indicates higher flood susceptibility.

### **3.2 Slope**

* Derived from DEM.
* Steeper slopes facilitate runoff, reducing flood risk; gentler slopes increase stagnation.

### **3.3 Flow Accumulation**

* Represents the number of upstream cells contributing flow to each pixel.
* Higher values indicate major drainage paths and potential flood runoff concentration.

### **3.4 Topographic Wetness Index (TWI)**

TWI is computed as:

[
\text{TWI} = \ln\left(\frac{\text{Catchment Area}}{\tan(\beta)}\right)
]

Where:

* **Catchment Area** = flow accumulation × cell size
* **β** = slope in radians

High TWI values imply higher moisture accumulation and flood potential.

### **3.5 Distance to River**

* Euclidean distance raster generated from river networks.
* Areas closer to rivers have higher exposure to fluvial flooding.

### **3.6 Precipitation**

* Source: CRU dataset (processed in ArcMap).
* Represents long-term monsoon rainfall averages.
* High rainfall regions correlate strongly with flood events.

### **3.7 Land Use / Land Cover (LULC)**

* Source: 
*   - :octocat: [LULC-Rangpur-2023 repository]([(https://github.com/Saeedsourav1/LULC-Rangpur-2023))])
* Flood risk varies by category:

  * Water bodies: very high risk
  * Agricultural land: moderate risk
  * Vegetation cover: low to moderate
  * Built-up areas: variable, often high due to imperviousness

### **3.8 Elevation-Derived Indicators**

* Additional parameters such as curvature, roughness, or local slope changes.
* Provide supplementary context for hydrological behavior.

---

# **4. Raster Preprocessing & Hydrological Derivation**

Ensuring consistency across all rasters is essential before analysis.


### **4.1 DEM Conditioning**

Performed using gee-hydrology-toolkit:

* Sink filling
* Flow direction (D8 algorithm)
* Flow accumulation
* TWI calculation

### **4.2 Reprojection**

All rasters were projected to:

* **UTM Zone 45N**
* Datum: WGS84
* Cell size:  30 m
* 8 bit pixel
* 

### **4.3 Clipping & Masking**

All datasets were clipped to the exact study boundary using `Clip Raster by Mask`.

### **4.4 Resampling**

If required, resampling nearest-neighbor was applied to maintain equal grid dimensions.

---

# **5. Standardization of Flood Conditioning Factors**

To combine variables of different units, each raster is standardized to a uniform scale. Here, a **1–5 suitability scale** was used:

* **5 = highest flood susceptibility**
* **1 = lowest flood susceptibility**


Here is a **professional, publication-ready table** in **Markdown format** that follows the same structure and styling as your reference images.
You can paste this directly into your **README.md** or **methodology.md**.

---

# **5.1 Flood Conditioning Factors, Subclasses, Area Coverage, Rank, and AHP Weight**


## **Table: Weighted Evaluation of Flood Conditioning Layers**
Below is the table rearranged **in descending order of weightage** for each layer.
Only the **main layers** are sorted by weight; subclasses remain unchanged.

---

| **Layer**                  | **Weight** | **Subclasses**  | **Area (km²)** | **Rank** |
| -------------------------- | ---------- | --------------- | -------------- | -------- |
| **Elevation (m)**          | **35%**    | -20 to 28.44    | 447.09         | 5        |
|                            |            | 28.44 to 39.58  | 512.09         | 4        |
|                            |            | 39.58 to 51.84  | 330.52         | 3        |
|                            |            | 51.84 to 68.54  | 250.07         | 2        |
|                            |            | 68.54 to 122    | 793.59         | 1        |
| **Slope (% rise)**         | **24%**    | < 1.36          | 78.19          | 1        |
|                            |            | 1.36 to 2.95    | 859.67         | 2        |
|                            |            | 2.95 to 4.76    | 3666.23        | 3        |
|                            |            | 4.76 to 8.17    | 7734.97        | 4        |
|                            |            | 8.17 to 58      | 3932.95        | 5        |
| **Flow accumulation**      | **15%**    | 0.69 to 1.36    | 9,984.38       | 1        |
|                            |            | 1.36 to 3.02    | 4,221.34       | 2        |
|                            |            | 3.02 to 5.40    | 1,240.71       | 3        |
|                            |            | 5.40 to 8.90    | 639.86         | 4        |
|                            |            | 8.90 to 14.82   | 205.17         | 5        |
| **Distance to Rivers (m)** | **10%**    | 0 to 1362       | 256.53         | 5        |
|                            |            | 1362 to 3212    | 1,253.07       | 4        |
|                            |            | 3212 to 5548    | 3,349.60       | 3        |
|                            |            | 5548 to 9344    | 5,700.60       | 2        |
|                            |            | 9344 to 24821   | 5,731.50       | 1        |
| **LULC**                   | **6%**     | Crops           | 190.10         | 4        |
|                            |            | Built-up        | 108.18         | 5        |
|                            |            | Water bodies    | 20.04          | 5        |
|                            |            | Bare ground     | 12.81          | 2        |
|                            |            | Vegetation      | 52.79          | 1        |
| **TWI**                    | **4%**     | < 4.08          | 8,321.13       | 1        |
|                            |            | 4.08 to 6.04    | 4,651.38       | 2        |
|                            |            | 6.04 to 8.71    | 2,233.05       | 3        |
|                            |            | 8.71–12.94      | 876.65         | 4        |
|                            |            | 12.94 to 20     | 189.79         | 5        |
| **NDVI**                   | **3%**     | -0.37 to -0.034 | 4,363.02       | 5        |
|                            |            | -0.034 to 0.23  | 7,245.82       | 4        |
|                            |            | 0.23 to 0.42    | 3,228.65       | 3        |
|                            |            | 0.42 to 0.53    | 1,054.72       | 2        |
|                            |            | 0.53 to 0.80    | 399.25         | 1        |
| **Precipitation (mm)**     | **2%**     | < 1047          | 4,140.95       | 1        |
|                            |            | 1412 to 1670    | 3,659.08       | 2        |
|                            |            | 1670 to 1928    | 3,875.44       | 3        |
|                            |            | 1928 to 2179    | 2,939.44       | 4        |
|                            |            | 2179 to 2651    | 1,676.44       | 5        |

---

### **Note**

**Rank interpretation:**
1 = Very Low, 2 = Low, 3 = Moderate, 4 = High, 5 = Very High

---


# **6. Analytical Hierarchy Process (AHP)**

AHP was used to assign objective weights to the eight factors.

---



## **6.2 Normalization & Weight Extraction**

Each value is divided by the column sum.
The average of each row gives the eigenvector weight.

![AHP Weight Formula](https://latex.codecogs.com/svg.latex?w_i%20=%20%5Cfrac%7B%5Csum_%7Bj=1%7D%5En%20a_%7Bij%7D' %7D%7Bn%7D)


---

## **6.3 Consistency Check**

AHP requires a consistency ratio < 0.10.

**Consistency Index (CI):**

![CI](https://latex.codecogs.com/svg.latex?CI%20=%20%5Cfrac%7B%5Clambda_%7Bmax%7D%20-%20n%7D%7Bn-1%7D)

**Consistency Ratio (CR):**

![CR](https://latex.codecogs.com/svg.latex?CR%20=%20%5Cfrac%7BCI%7D%7BRI%7D)

Where:

- \( \lambda_{\text{max}} \) = maximum eigenvalue  
- **RI** = Random Index

If CR > 0.10, the matrix must be revised.

---

# **7. Flood Susceptibility Index (FSI) Computation**

The Weighted Linear Combination (WLC) model integrates all standardized rasters:

![FSI](https://latex.codecogs.com/svg.latex?FSI%20=%20%5Csum_{i=1}^{8}%20(w_i%20%5Ccdot%20f_i))

Where:

- \( w_i \) = Weight of factor *i*  
- \( f_i \) = Standardized raster value


This produces a continuous raster surface representing flood likelihood.

---

# **8. ArcMap Computation Workflow**

### **8.1 Weighted Overlay Method**

Suitable when using 1–5 classified rasters.

Steps:

1. Open **Weighted Overlay** tool.
2. Add standardized rasters.
3. Assign AHP weights.
4. Run to generate the susceptibility map.

### **8.2 Raster Calculator Method**


Formula:

```
("FSS_temp" = 0.35*(6 - "Elevation") + 0.24*"Slope" + 0.02*"PREC" + 0.15*"FlowAcc" + 0.1*"DTR" + 0.06*"LULC" + 0.03*(6 - "NDVI") + 0.04*"TWI")
```

The output is a continuous FSI raster.

In this section I have used raster calculator method

---


# **9. Classification of Susceptibility Zones**

The continuous FSI map is reclassified into five classes:

* Very Low
* Low
* Moderate
* High
* Very High

Thresholds were determined using:

* Quantile classification

The resulting zonation map communicates spatial flood risk levels.

---

# **10. Area Assessment of Susceptibility Classes**

To quantify vulnerability:

**Area Calculation Formula**

![Area Formula](https://latex.codecogs.com/svg.latex?%5Ctext{Area}_{class}%20=%20N_{pixels}%20%5Ctimes%20(%5Ctext{Cell%20Size})^2)

Where:

- \( N_{pixels} \) = Count of pixels within each class


Outputs include:

* Total area under each susceptibility class
* Percentage distribution of flood zones

This supports policymakers in understanding the extent of high-risk regions.


# **12. Final Outputs**

The analysis produces:

* Flood Susceptibility Index (FSI) raster
* 5-class hazard zonation map
* AHP weight table
* Class-wise area distribution report
* High-quality maps for publication

---
