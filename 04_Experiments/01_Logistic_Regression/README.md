# Logistic Regression — English Baselines

This directory documents the logistic regression baselines evaluated for multilabel narrative classification in English news.

## Evaluated Models

Three TF-IDF representations were compared using one-vs-rest logistic regression:

| Model | Coarse F1 | Fine F1 |
|---|---:|---:|
| Word TF-IDF + Logistic Regression | 0.4731 | 0.4282 |
| Character TF-IDF + Logistic Regression | 0.4670 | 0.4252 |
| Word + Character TF-IDF + Logistic Regression | 0.4782 | 0.4233 |

All results are based on the same 399 English held-out documents across three outer folds, with thresholds selected on inner validation.

## Experimental Artifacts

The original output archives are:

- `baseline_EN_v1_foldall3_seed42_95db0632ddb.zip`
- `baseline_char_EN_v1_foldall3_seed42_d4e10a56178d.zip`
- `baseline_hybrid_EN_v1_foldall3_seed42_298ffe0ee938.zip`

## Download

The complete experimental artifacts are included in `Rare_Narratives.rar`, available under:

[GitHub Release v1.0.0](https://github.com/Nizar-099/rare-narratives-nlp/releases/tag/v1.0.0)

Inside the downloaded archive, navigate to `04_Experiments/01_Logistic_Regression/`.

For the complete mapping between published results and experimental artifacts, see `06_Documentation/EXPERIMENT_INDEX.md`.
