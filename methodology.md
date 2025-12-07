# 📄 **Methodology for Flood Susceptibility Mapping Using AHP and Multi-Criteria GIS Analysis**

## **1. Introduction**

Flood susceptibility mapping aims to quantify the spatial likelihood of flooding based on terrain, hydrological, climatic, and land-use characteristics. This study employs the **Analytical Hierarchy Process (AHP)** integrated with GIS-based multi-criteria evaluation to assess flood-prone zones in the Rangpur Division of Bangladesh.

AHP provides a structured framework for determining the relative importance of multiple flood-conditioning factors. GIS then spatially applies these weights to generate a Flood Susceptibility Index (FSI).

---

# **2. Overall Workflow**

The methodological framework consists of:

1. Data Collection
2. Raster Preprocessing & Hydrological Derivation
3. Standardization of Conditioning Factors
4. AHP Weight Calculation
5. Weighted Linear Combination (WLC) Modelling
6. Flood Susceptibility Classification
7. Area-Based Assessment

---

# **3. Data Collection & Description of Flood Conditioning Factors**

Eight conditioning factors were selected based on hydrological relevance and literature support.

---

### **3.1 Digital Elevation Model (DEM)**

* Source: GEE Hydrology Toolkit
* Governs elevation gradients, depressions, and drainage pathways.

---

### **3.2 Slope**

* Derived from DEM.
* Gentle slopes increase water stagnation; steep slopes disperse runoff.

---

### **3.3 Flow Accumulation**

* Represents upstream contributing cells.
* High values indicate channels or flow convergence zones.

---

### **3.4 Topographic Wetness Index (TWI)**

TWI is computed as:

![TWI](https://latex.codecogs.com/svg.latex?TWI%20=%20%5Cln%20%5Cleft\(%20%5Cfrac%7B%5Ctext%7BCatchment%20Area%7D%7D%7B%5Ctan%28%5Cbeta%29%7D%20%5Cright\))

Where:

* **Catchment Area** = Flow Accumulation × Cell Size
* **β** = Slope in radians

High TWI indicates moisture concentration.

---

### **3.5 Distance to River (DTR)**

* Euclidean distance from river network.
* Lower distances imply higher fluvial flood exposure.

---

### **3.6 Precipitation**

* Source: CRU rainfall dataset processed in ArcMap.
* Represents long-term monsoon rainfall.

---

### **3.7 Land Use / Land Cover (LULC)**

* Source:
  🔗 [https://github.com/Saeedsourav1/LULC-Rangpur-2023](https://github.com/Saeedsourav1/LULC-Rangpur-2023)

Flood response varies by class:

* Water bodies → Very High
* Agriculture → Moderate
* Vegetation → Low
* Built-up → Variable (often high due to imperviousness)

---

### **3.8 Elevation-Derived Indicators**

Includes curvature, roughness, and micro-terrain attributes supporting hydrological behavior.

---

# **4. Raster Preprocessing & Hydrological Derivation**

All rasters were standardized to ensure uniform spatial and analytical conditions.

---

### **4.1 DEM Conditioning**

Using GEE Hydrology Toolkit:

* Sink Fill
* Flow Direction (D8)
* Flow Accumulation
* TWI Generation

---

### **4.2 Reprojection**

All layers were projected to:

* **UTM Zone 45N (WGS84)**
* Resolution: **30 m**
* Pixel depth: **8-bit**

---

### **4.3 Clipping & Masking**

* Applied using *Clip Raster by Mask* to ensure exact study area boundaries.

---

### **4.4 Resampling**

* Nearest-neighbor method used where necessary to maintain raster alignment.

---

# **5. Standardization of Flood Conditioning Factors**

All factors were reclassified into a **1–5 suitability scale**:

| Value | Meaning                  |
| ----- | ------------------------ |
| **5** | Very High Susceptibility |
| **4** | High                     |
| **3** | Moderate                 |
| **2** | Low                      |
| **1** | Very Low                 |

---

# **5.1 Weighted Evaluation of Flood Conditioning Layers**

Your full table is preserved exactly as constructed.
(Already GitHub-compatible — no LaTeX used.)

---

# **6. Analytical Hierarchy Process (AHP)**

AHP was applied to derive relative weights for all eight conditioning factors.

---

## **6.2 Normalization & Weight Extraction**

Weight calculation formula:

![AHP Weight Formula](https://latex.codecogs.com/svg.latex?w_i%20=%20%5Cfrac%7B%5Csum_%7Bj=1%7D%5En%20a_%7Bij%7D%27%7D%7Bn%7D)

Where:

* ( a_{ij}' ) = normalized pairwise value
* ( n ) = number of factors

---

## **6.3 Consistency Check**

AHP requires **CR < 0.10**.

**Consistency Index (CI):**

![CI](https://latex.codecogs.com/svg.latex?CI%20=%20%5Cfrac%7B%5Clambda_%7Bmax%7D%20-%20n%7D%7Bn-1%7D)

**Consistency Ratio (CR):**

![CR](https://latex.codecogs.com/svg.latex?CR%20=%20%5Cfrac%7BCI%7D%7BRI%7D)

Where:

* ( \lambda_{\text{max}} ) = Maximum eigenvalue
* **RI** = Random Index

If **CR > 0.10**, the matrix must be revised.

---

# **7. Flood Susceptibility Index (FSI) Computation**

Weighted Linear Combination (WLC):

![FSI](https://latex.codecogs.com/svg.latex?FSI%20=%20%5Csum_%7Bi=1%7D%5E8%20%28w_i%20%5Ccdot%20f_i%29)

Where:

* ( w_i ) = AHP weight of factor *i*
* ( f_i ) = Standardized raster

---

# **8. ArcMap Computation Workflow**

### **8.1 Weighted Overlay Method**

1. Add standardized rasters.
2. Assign AHP weights.
3. Execute Weighted Overlay tool.

---

### **8.2 Raster Calculator Method**

```txt
"FSS_temp" = 0.35*(6 - "Elevation") + 0.24*"Slope" + 0.02*"PREC" 
           + 0.15*"FlowAcc" + 0.1*"DTR" + 0.06*"LULC" 
           + 0.03*(6 - "NDVI") + 0.04*"TWI"
```

Produces a continuous flood susceptibility surface.

---

# **9. Classification of Susceptibility Zones**

The FSI raster is classified using **quantiles** into:

* Very Low
* Low
* Moderate
* High
* Very High

---

# **10. Area Assessment of Susceptibility Classes**

Area calculation formula:

![Area Formula](https://latex.codecogs.com/svg.latex?%5Ctext{Area}_{class}%20=%20N_{pixels}%20%5Ctimes%20%28%5Ctext{Cell%20Size}%29%5E2)

Where:

* ( N_{pixels} ) = Number of pixels in each class

Outputs include:

* Total area per class
* Class-wise percentage distribution

---

# **12. Final Outputs**

The workflow generates:

* Flood Susceptibility Index raster
* Five-class susceptibility map
* AHP-derived weight table
* Area distribution statistics
* Publication-ready maps and documentation

---

