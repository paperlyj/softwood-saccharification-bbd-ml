# Reproducibility files for steam-exploded softwood saccharification

This repository contains the data and analysis code supporting the manuscript:

**Optimization of saccharification in steam-exploded softwood using statistical and machine learning approaches**

## Scope

The repository provides the analysis files used for the revised BBD–RSM and machine-learning workflow, with particular emphasis on the fully nested **condition-level** validation requested during peer review.

The final ML validation uses:

- bark-free dataset: **23 unique factor conditions**
- bark-containing dataset: **29 unique factor conditions**
- outer validation: **leave-one-condition-out cross-validation (LOOCV)**
- inner model selection: **5-fold cross-validation**
- inner optimization criterion: **RMSE**
- all data-dependent preprocessing and hyperparameter selection performed exclusively within each outer-training fold

The individual experimental responses are also provided so that the aggregation from raw independent responses to condition-level ML samples can be audited directly.

## Repository contents

```text
.
├── BBD_ML_reproducibility.ipynb
├── README.md
├── requirements.txt
├── data/
│   ├── DATA_DICTIONARY.md
│   ├── raw_without_bark.xlsx
│   ├── raw_with_bark.xlsx
│   ├── individual_responses_without_bark.csv
│   ├── individual_responses_with_bark.csv
│   ├── condition_level_without_bark.csv
│   └── condition_level_with_bark.csv
├── results/
│   └── reported_table4_metrics.csv
└── figures/
```

## Data organization

Each row of the individual-response CSV files represents one independent saccharification experiment. The duplicate HPLC technical measurements associated with each independent experiment were averaged before inclusion in the analysis dataset.

For ML validation, all independent responses sharing the same combination of:

1. total enzyme loading,
2. substrate concentration, and
3. KMF006 blending ratio

were aggregated to one condition-level response before cross-validation.

This prevents an identical factor combination from appearing simultaneously in the outer training and test sets.

## Main reported ML results

| Bark condition | Model with numerically highest R² / lowest RMSE | R² | RMSE | MAE | MRE |
|---|---|---:|---:|---:|---:|
| Without bark | SVR | 0.668 | 4.986 | 3.418 | 0.059 |
| With bark | SplineRidge | 0.459 | 4.434 | 3.148 | 0.057 |

Complete model results are provided in `results/reported_table4_metrics.csv`.

## Reproducing the analysis

Create a Python environment and install the required packages:

```bash
pip install -r requirements.txt
```

Then open:

```text
BBD_ML_reproducibility.ipynb
```

and execute the cells from top to bottom.

The notebook contains:

1. BBD–RSM reanalysis using the independent experimental responses;
2. response-surface plotting;
3. audit of the individual ML observations;
4. aggregation to 23 and 29 unique condition-level samples;
5. fully nested condition-level LOOCV;
6. hyperparameter-selection audit;
7. generation of the revised ML figures.

Because the fully nested procedure performs model selection independently in every outer fold, the complete run can take substantial computation time, particularly for Gaussian process regression.

## Reproducibility note

The repository notebook intentionally contains the **final analysis supporting the revised manuscript** rather than exploratory model-screening or superseded run-level validation workflows. This avoids ambiguity between development analyses and the condition-level nested validation used for the reported results.

## Citation

If this repository is used, please cite the associated article after publication.

## Contact

For questions regarding the analysis, please contact the corresponding author listed in the manuscript.
