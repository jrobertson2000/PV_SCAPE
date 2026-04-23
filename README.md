# PV_SCAPE (Open‑Source)

**PV Screening Capacity & Energy (PV_SCAPE)** models spatially explicit photovoltaic energy capacity and production potential for pivot corners, canals, and commercial rooftops.

This version is built for **enterprise Windows environments** to avoid issues of locked‑down
permissions and uses that arise when using Esri's proprietary arcpy python packages:

PV_SCAPE utilizes:
- GeoPandas for spatial data
- PySAM (NREL) for PVWatts v8
- CSV artifacts for weather mapping and QA
- Explicit preset‑driven configuration

---

## Repository Structure
pv_scape/
│
├─ README.md                     # Main documentation (required)
├─ requirements.txt              # Python dependencies
├─ PV_SCAPE_opensource_v2.ipynb  # Main notebook
├─ PV_SCAPE_preprocess1_required_for_canal_assessment.ipynb             # Preprocess required only for canals or other narrow, linear sites
├─ PV_SCAPE_preprocess2_required_for_input_area_and_yield_fields.ipynb  # Preprocess required for all input features
├─ PV_SCAPE_preprocess3_required_for_PVWatts_integration.ipynb          # Preprocess required to download weather data for PVWatts integration
├─ arcgis_to_gpkg.py             # Preprocess bridge script to export input feature class from Esri ArcGIS File Geodatabase to opensource GeoPackage
├─ gpkg_to_arcgis.py             # Postprocess bridge script to export final feature class back to Esri ArcGIS File Geodatabase from opensource GeoPackage
├─ solar_feasibility_structured_v7.ipynb    # Postprocess plotting of outputs (capacity and energy per area)
├─ ARCPY_LCS_overlap_summary_stats.ipynb    # Helper to assign WSU Least Conflict Solar values to input features
│
└─ data/                         # (not yet filled)
   └─ .gitkeep                   # (placeholder for folder tracking)
