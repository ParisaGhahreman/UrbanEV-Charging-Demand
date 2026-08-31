# Data sources and access

## CHARGED

The CHARGED data are used as the development and internal-validation source. They are not redistributed here. Obtain the data from the original provider or publication under its applicable access and reuse terms, then place the supplied archive in:

```text
data/raw/charged/Hourly.zip
```

## UrbanEV (Shenzhen)

UrbanEV is used only for the independent external evaluation. It is not used for training, model selection, hyperparameter tuning, or threshold selection. The source data are not redistributed in this repository. After obtaining them through the original source, place them under:

```text
data/raw/urbanev/
```

## GHSL

The Isfahan exploratory workflow uses 2020 GHSL population and built-surface rasters. Obtain the relevant GHSL files under their provider terms and place them in:

```text
data/raw/ghsl/
```

## OpenStreetMap data

Roads, points of interest, administrative boundaries, existing mapped charging features, and screening features for Isfahan are retrieved from OpenStreetMap during notebook execution. OSM data are time-dependent and subject to the Open Database License (ODbL). Record the retrieval date when reproducing the workflow.

## Important reproducibility note

The public repository excludes raw data, intermediate geospatial files, and raster files because of source-data conditions and file size. The included notebooks, trained models, derived non-restricted outputs, figures, and audit tables document the analytical workflow and reported findings.
