# Spatial Analysis of Mental Health Outcomes in US Counties

## Project Overview
This comprehensive spatial analysis examines the relationship between mental health outcomes (depression and mental distress), social vulnerability, and chronic disease prevalence across US counties( Two primary composite indices the Social Vulnerability Index (SVI) computed as the average of normalized social determinant variables, and the Comorbidity Risk Index (CRI) calculated as the means of normalized chronic health condition variables). The project employs advanced spatial statistics and econometric methods to identify clusters, model relationships, and simulate policy interventions.

##Objectives
- Identify spatial clusters of depression and mental distress using Local Indicators of Spatial Association (LISA)
- Bivariate Plot of Mental Health outcomes and Social Vulnerability Index (SVI) and Comorbidity Risk Index (CRI)
- Model spatially varying relationships using Geographically Weighted Regression (GWR)
- Simulate policy interventions using Monte Carlo methods with spatial spillovers
- Provide evidence-based insights for targeted public health interventions

## Data Sources

### Primary Dataset
- **File**: `complete_mental_health_counties.shp` (The primary data source for this project will be the CDC PLACES dataset (2024 release))
- **Content**: US county-level data with geometry and multiple indicators
- **Variables Included**:
  - `depress`: Depression prevalence rates (%)
  - `mentdist`: Mental distress prevalence rates (%)
  - `svi`: Social Vulnerability Index
  - `cri`: Chronic Risk Index or Chronic Disease Prevalence
  - Geographic coordinates and county boundaries

### Data Characteristics
- **Spatial Scale**: County-level
- **Temporal Scope**: Cross-sectional data
- **Geographic Coverage**: Contiguous United States (initial file has all but for our analysis i have limited it  for contiguous US)
- **Projection**: US Albers Equal Area Conic projection for spatial analysis

## Methodology

### 1. Exploratory Spatial Data Analysis (ESDA)
- **Spatial Weights**: Queen contiguity weights matrix
- **Cluster Detection**: Local Moran's I (LISA) for hotspot identification
- **Visualization**: Choropleth maps, bivariate maps, cluster maps

### 2. Spatial Regression Modeling
- **Geographically Weighted Regression (GWR)**: Models local relationships between mental health outcomes and predictors
- **Bandwidth Selection**: Adaptive bandwidth using AICc optimization
- **Model Diagnostics**: Local R², coefficient maps

### 3. Policy Simulation
- **Monte Carlo Methods**: 1000 iterations with parameter uncertainty
- **Spatial Spillovers**: 30% effect diffusion to neighboring counties
- **Intervention Scenarios**: 5%, 10%, 15% reductions in chronic risk factors
- **Impact Assessment**: Confidence intervals, county-level effects

## Technical Implementation

### Required Libraries
```python
# Core data analysis
import numpy as np
import pandas as pd
import geopandas as gpd

# Visualization
import matplotlib.pyplot as plt
import matplotlib.patches as patches
from matplotlib.patches import Patch

# Spatial analysis
import mapclassify
from libpysal.weights import Queen
from esda.moran import Moran_Local, Moran

# Spatial econometrics
from mgwr.gwr import GWR
from mgwr.sel_bw import Sel_BW

# Utilities
from sklearn.preprocessing import MinMaxScaler
from shapely.geometry import Point

# Advanced mapping
import cartopy.crs as ccrs
import cartopy.feature as cfeature
```

### Analysis Pipeline
1. **Data Preparation**: Loading, cleaning, and projecting spatial data
2. **Spatial Weights**: Creating neighborhood structure
3. **Cluster Analysis**: Identifying significant hotspots and coldspots
4. **GWR Modeling**: Estimating local relationships
5. **Monte Carlo Simulation**: Policy impact assessment with uncertainty
6. **Visualization**: Creating publication-quality maps and results

## Key Analyses

### A. Cluster Analysis
- High-High clusters (hotspots): Areas with high values surrounded by high values
- Low-Low clusters (coldspots): Areas with low values surrounded by low values
- Spatial outliers: High-Low and Low-High patterns

### B. Bivariate Analysis (plot)
- Depression vs. Social Vulnerability
- Depression vs. Chronic Disease
- Mental Distress vs. Social Vulnerability  
- Mental Distress vs. Chronic Disease

### C. Policy Simulations
- Targeted interventions in identified hotspots
- Quantification of direct and spillover effects
- Uncertainty estimation through Monte Carlo methods

## Key Insights
- Identification of statistically significant mental health clusters
- Spatial variation in relationships between predictors and outcomes
- Quantified impacts of potential public health interventions
- Evidence for targeted rather than uniform policy approaches

## Applications
- Public health policy planning
- Resource allocation optimization
- Targeted intervention design
- Spatial epidemiology research
- Health equity analysis

## Limitations
- Cross-sectional analysis (no temporal dynamics)
- Modifiable Areal Unit Problem (MAUP)
- Assumptions in spatial weights structure
- Data quality and completeness at county level