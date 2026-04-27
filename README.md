# PV_SCAPE (Open‑Source)

**PV Screening Capacity & Energy (PV_SCAPE)** models spatially explicit photovoltaic energy capacity and production potential for pivot corners, canals, and commercial rooftops.

This version is built for **enterprise Windows environments** to avoid issues of locked‑down
permissions and uses that arise when using Esri's proprietary arcpy python packages:

PV_SCAPE utilizes:
- GeoPandas for spatial data
- PySAM (NREL) for PVWatts v8
- CSV artifacts for weather mapping and QA
- Explicit preset‑driven configuration

## Environment policy:
ArcGIS Pro Python (proprietary):
  Used only for arcpy and exporting to GPKG/CSV.

venv_PV_SCAPE (opensource):
  Used for all PV_SCAPE notebooks, PVWatts/PySAM runs,
  geopandas processing, and feasibility analysis.

solar-clean is deprecated.

## Coordinate Reference System (CRS) Contract
PV_SCAPE enforces a strict CRS contract to ensure consistent and correct 
results across rooftop, canal, and ground‑mounted datasets. Running screening
calculations in a geographic CRS (degrees) can silently produce incorrect or
empty results, especially for rooftops. This contract prevents unit errors 
and ensures consistent behavior across all PV types.

Canonical CRSs:

Projected CRS (authoritative):
EPSG:2927 — NAD83(HARN) / Washington South (ftUS)
Used for all physical calculations (area, length, capacity).

Geographic CRS (derived):
EPSG:4326 — WGS84
Used only for latitude/longitude and weather station matching.

Internal representation
PV_SCAPE maintains two GeoDataFrames after loading inputs:

gdf_proj — projected, authoritative geometry
gdf_geo — geographic copy derived from gdf_proj

All capacity, screening, and numeric geometry operations use gdf_proj.
gdf_geo is used exclusively for weather lookup and reporting coordinates.
Why this matters


## Repository Structure
pv_scape/
│
├─ README.md                                                            # Main documentation (required)
├─ requirements.txt                                                     # Python dependencies
├─ PV_SCAPE_opensource_v3.ipynb                                         # (opensource) Main notebook
├─ PV_SCAPE_preprocess1_required_for_canal_assessment.ipynb             # Preprocess required only for canals or other narrow, linear sites
├─ PV_SCAPE_preprocess2_required_for_input_area_and_yield_fields.ipynb  # Preprocess required for all input features
├─ PV_SCAPE_preprocess3_required_for_PVWatts_integration.ipynb          # Preprocess required to download weather data for PVWatts integration
├─ arcgis_to_gpkg.py                                                    # (arcpy required) Preprocess bridge script to export input feature class from Esri ArcGIS File Geodatabase to opensource GeoPackage
├─ PV_SCAPE_merge_outputs.py                                            # (opensource) Postprocess merging the GeoPackage feature classes into a new GeoPackage single feature class
├─ PV_SCAPE_postprocess_spatial_attribution.ipynb                       # (opensource) Postprocess to enrich the PV_SCAPE output in prep for aggregate feasibility analysis
├─ solar_feasibility_structured_v7.ipynb                                # (opensource) Postprocess plotting of outputs (capacity and energy per area)
├─ gpkg_to_arcgis.py                                                    # (arcpy required) Postprocess bridge script to export final feature class back to Esri ArcGIS File Geodatabase from opensource GeoPackage
│
├─ ARCPY_LCS_overlap_summary_stats.ipynb                                # (arcpy required) Helper to assign WSU Least Conflict Solar values to input features
│
└─ data/                         # (not yet filled)
   └─ .gitkeep                   # (placeholder for folder tracking)
