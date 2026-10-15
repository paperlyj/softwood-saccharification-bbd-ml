# Data dictionary

## Individual-response files
`individual_responses_without_bark.csv` and `individual_responses_with_bark.csv`

- `Bark_condition`: bark-free or bark-containing substrate.
- `Observation_ID`: unique identifier for each independent saccharification response.
- `Experimental_Run`: original nominal experimental run identifier.
- `Independent_replicate`: independent saccharification replicate number within a run.
- `Source`: original BBD run or supplementary experiment.
- `Condition_ID`: unique factor-combination identifier.
- `FPU`: total enzyme loading (FPU/g-glucan).
- `Substrate`: substrate concentration (%, w/v).
- `KMF006_ratio_percent`: KMF006 blending ratio based on FPU activity (%).
- `Saccharification_yield_percent`: measured saccharification yield (%).

Each row represents one independent saccharification experiment. Duplicate HPLC technical measurements were averaged before the value was entered into the analysis dataset.

## Condition-level files
`condition_level_without_bark.csv` and `condition_level_with_bark.csv`

All independent responses sharing the same combination of FPU, substrate concentration, and KMF006 blending ratio were aggregated before ML validation.

- Bark-free dataset: 54 individual responses -> 23 unique conditions.
- Bark-containing dataset: 68 individual responses -> 29 unique conditions.

These condition-level datasets are the independent units used for the fully nested condition-level LOOCV reported in the revised manuscript.
