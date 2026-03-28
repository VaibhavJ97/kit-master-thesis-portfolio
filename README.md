# Impact of Climate Change on the Geothermal Potential of Closed Systems Using GIS and Python

## Overview

This project presents a Python-based Jupyter Notebook workflow for assessing the geothermal potential of **single borehole heat exchanger (BHE)** systems across Germany under **CMIP6 climate scenarios**.

The notebook combines:
- geothermal heat extraction modeling
- GeoTIFF-based climate raster processing
- scenario-based comparison for **SSP2-4.5** and **SSP5-8.5**
- interactive **Folium** map visualization
- ensemble statistics across multiple climate model inputs

The aim is to estimate how climate-driven subsurface temperature changes may influence the **technical** and **sustainable** geothermal potential of closed-loop systems over time.

---

## Project Objectives

The main objectives of this project are:

- to evaluate the geothermal performance of a **single BHE system**
- to compare model outputs under different CMIP6 climate scenarios
- to calculate **heat extraction rates** and **usable power**
- to generate interactive geospatial maps for Germany
- to create ensemble-based visual summaries such as:
  - mean
  - 25th percentile
  - 50th percentile
  - 75th percentile

---

## Main Features

- Python-based geothermal modeling workflow
- GeoTIFF raster input processing with `rasterio`
- Germany boundary integration using `geopandas`
- Numerical solution of heat extraction and sustainability functions using `scipy`
- Interactive web maps using `folium`
- Comparison of multiple climate model outputs
- Visualization of:
  - maximum heat extraction rate `[W/m]`
  - sustainable heat extraction rate `[W/m]`
  - usable geothermal power `[W]`

---

## Notebook Contents

The notebook includes the following key components:

1. **Import and preprocessing**
   - scientific Python libraries
   - Germany boundary loading
   - raster input handling

2. **Thermal model functions**
   - mean fluid temperature calculations
   - infinite plane and initial temperature functions
   - sustainability-based extraction rate estimation

3. **Model parameter definition**
   - thermal diffusivity
   - borehole depth
   - borehole spacing
   - radius and resistance parameters
   - 50-year and 100-year simulation horizons

4. **GeoTIFF-based scenario analysis**
   - loading and downsampling climate rasters
   - pixel-wise model computation
   - technical and sustainable potential mapping

5. **Interactive map generation**
   - custom Folium overlays
   - legends and colorbars
   - scenario-specific map layers

6. **Ensemble statistics**
   - mean
   - 25th percentile
   - median
   - 75th percentile

---

## Input Data

This project uses climate-based raster inputs in **GeoTIFF** format for Germany.

Example input files:
- `BBC_ssp245_2000_2100_Germany_mean.tif`
- `BBC_ssp585_2000_2100_Germany_mean.tif`
- `CanESM_ssp245_2000_2100_Germany_mean.tif`
- `CanESM_ssp585_2000_2100_Germany_mean.tif`
- `GFDL_ssp245_2000_2100_Germany_mean.tif`
- `GFDL_ssp585_2000_2100_Germany_mean.tif`
- `GISS_ssp245_2000_2100_Germany_mean.tif`
- `GISS_ssp585_2000_2100_Germany_mean.tif`
- `HadGEM_ssp245_2000_2100_Germany_mean.tif`
- `HadGEM_ssp585_2000_2100_Germany_mean.tif`
- `IPSL_ssp245_2000_2100_Germany_mean.tif`
- `IPSL_ssp585_2000_2100_Germany_mean.tif`
- `MIROC_ssp245_2000_2100_Germany_mean.tif`
- `MIROC_ssp585_2000_2100_Germany_mean.tif`
- `MPI_ssp245_2000_2100_Germany_mean.tif`
- `MPI_ssp585_2000_2100_Germany_mean.tif`

---

## Technologies Used

- Python
- Jupyter Notebook
- NumPy
- Matplotlib
- Rasterio
- SciPy
- Joblib
- Folium
- GeoPandas
- IPython Display

---

## Output

The project generates:
- geothermal performance maps
- interactive Folium-based visualizations
- scenario comparison layers
- ensemble-based statistical maps for Germany

You can also export map results as `.html` files for direct viewing in a browser.

---

## Example Visual Outputs

Add screenshots here from your generated maps.

Example:

```md
![SSP245 Map Preview](outputs/images/preview_1.png)
![SSP585 Map Preview](outputs/images/preview_2.png)
