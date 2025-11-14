# Wildfire Monitoring -- Portugal (ETL Workflow)

This repository contains an end-to-end workflow for **extracting, transforming, and loading (ETL)** Earth observation data to support wildfire monitoring and environmental analysis in Portugal.

The project integrates multiple geospatial datasets from **Google Earth Engine (GEE)** and **Meteostat** to generate per-tile environmental indicators (NDVI, soil moisture, brightness temperature, and local weather conditions).

Note: 
- All heavy computations are performed on servers such **Google Earth Engine** or **Meteostat**.
- You can reproduce the environment using.
```bash
conda env create -f environment.yml -n fire-etl
conda activate fire-etl
```
## Project Structure

```
├── data/
│   ├── csv/          # Processed exports from Earth Engine & Meteostat
│   ├── geojson/      # Country grid and geometry inputs
│   └── ...
├── extract_transform_load_data_1.ipynb
├── extract_transform_load_data_2.ipynb
├── environment.yml   # Conda environment definition
├── .gitignore        # Ignore large data & temp files
└── README.md
```

## Data Sources

| Dataset | Description | Source |
|----------|--------------|--------|
| **MODIS MOD13Q1 v6.1** | 16-day NDVI, 250 m resolution | [NASA / MODIS](https://developers.google.com/earth-engine/datasets/catalog/MODIS_061_MOD13Q1) |
| **SMAP SPL3SMP_E (v005–v006)** | 9 km enhanced soil moisture, merged across versions | [NASA SMAP](https://developers.google.com/earth-engine/datasets/catalog/NASA_SMAP_SPL3SMP_E_006) |
| **FIRMS / MODIS T21** | Brightness temperature per detected fire pixel | [NASA FIRMS](https://firms.modaps.eosdis.nasa.gov/) |
| **Meteostat Daily** | Local weather (temperature, precipitation, etc.) | [Meteostat API](https://dev.meteostat.net/python/) |



## Setup

### 1. Run the ETL notebooks

Execute the notebooks in order:

- `extract_transform_load_data_1.ipynb`: Create the grid and export NDVI, SMAP, FIRMS data per tile.
- `extract_transform_load_data_2.ipynb`: Retrieve weather conditions from Meteostat for each tile.
