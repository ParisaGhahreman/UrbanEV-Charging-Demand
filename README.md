# UrbanEV Charging Demand

## Transferability Assessment for EV-Charging Demand Potential Modelling

This repository contains the reproducible workflow for a cross-city assessment of machine-learning models for estimating spatial electric-vehicle (EV) charging-demand potential. The study trains and evaluates models using CHARGED city data, performs an untouched external evaluation using UrbanEV data from Shenzhen, and prepares an exploratory spatial-data workflow for Isfahan, Iran.

> Main finding: although `HistGradientBoostingClassifier` performed best in internal leave-one-city-out validation, it did not transfer successfully to Shenzhen. Accordingly, this repository does **not** present the Isfahan model outputs as validated demand estimates or construction recommendations. The negative external-validation result is a central scientific result of the project.

## Study workflow

1. Audit CHARGED source data.
2. Engineer daily station/cell targets and transferable features.
3. Audit the independent UrbanEV Shenzhen data.
4. Harmonize the spatial analytical scale across datasets.
5. Train and compare models with leave-one-city-out validation on CHARGED only.
6. Evaluate the selected model once on UrbanEV Shenzhen, without training, tuning, or threshold selection on UrbanEV.
7. Prepare Isfahan spatial layers and document the limits of direct model transfer.

## Key result

The selected internal model was `HistGradientBoostingClassifier` with `learning_rate=0.05`, `max_iter=300`, `max_leaf_nodes=7`, `l2_regularization=1.0`, and `random_state=42`.

| Evaluation setting | ROC-AUC | PR-AUC | Top-20% precision |
|---|---:|---:|---:|
| Internal leave-one-city-out CHARGED | 0.5671 | 0.2905 | 0.3056 |
| External UrbanEV Shenzhen | 0.4773 | 0.2100 | 0.1786 |
| Random-selection prevalence benchmark | 0.5000 | 0.2036 | 0.2036 |

The external result is below the random-selection benchmark for the operational Top-20% metric. This indicates that the available general spatial features are insufficient for direct cross-city transfer without local calibration data.

## Repository structure

```text
UrbanEV_Charging_Demand/
├── notebooks/        # Six notebooks, to be run in numerical order
├── outputs/
│   ├── figures/      # Publication-ready figures
│   ├── models/       # Trained model artefacts
│   └── tables/       # Audits, model results, and predictions
├── docs/             # Master documentation and data-source notes
├── data/             # Local data only; excluded from the public repository
├── README.md
├── requirements.txt
├── LICENSE
├── CITATION.cff
└── .gitignore
```

## Notebooks

| Notebook | Purpose |
|---|---|
| `01_CHARGED_Data_Audit.ipynb` | CHARGED source-data audit |
| `02_CHARGED_Feature_Engineering.ipynb` | Daily targets and features |
| `03_UrbanEV_External_Data_Audit.ipynb` | Independent UrbanEV audit |
| `04_Cross_City_Spatial_Harmonization.ipynb` | Spatial harmonization and transfer contract |
| `05_CHARGED_Model_Training_and_City_Holdout.ipynb` | Internal validation, model selection, external evaluation, and shift analysis |
| `06_Isfahan_Case_Study_and_Siting.ipynb` | Exploratory Isfahan spatial-data preparation and screening workflow |

## Reproducibility

Create an environment and install dependencies:

```bash
conda create -n urban-ev python=3.11
conda activate urban-ev
pip install -r requirements.txt
```

Source data are not redistributed in this repository. After obtaining the source datasets under their original terms, place them in the paths described in `docs/DATA_SOURCES.md`, then run the notebooks in numerical order. The notebooks locate the project root dynamically and save generated outputs under the root-level `outputs/` directory.

## Data availability and restrictions

Raw CHARGED and UrbanEV data, as well as large derived geospatial files, are excluded from the public repository. They remain subject to the conditions of their original providers. The repository includes code, non-restricted derived audit outputs, trained model artefacts, and figures required to inspect the analysis.

## Limitations

- The Isfahan analysis has no observed local charging-demand labels; it is not a local validation study.
- OpenStreetMap-derived layers can be incomplete or time-dependent.
- Road proximity and spatial screening do not establish land ownership, electrical-grid capacity, permits, safety, parking feasibility, or construction cost.
- The project therefore reports a rigorous transferability assessment, not a validated final siting plan for Isfahan.

## Citation

If you use this repository, please cite the software metadata in [`CITATION.cff`](CITATION.cff). A Zenodo DOI will be added after the first GitHub release.

## DOI

The archived release of this repository is available through Zenodo:

[https://doi.org/10.5281/zenodo.22207854](https://doi.org/10.5281/zenodo.22207854)

## License

Code and derived non-restricted outputs are released under the [MIT License](LICENSE).
