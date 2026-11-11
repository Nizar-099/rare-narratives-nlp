# Standard SVM — English Baselines

This directory documents the standard Support Vector Machine (SVM) experiments for multilabel narrative classification in English news.

## Overview

Three lexical feature representations were evaluated using one-vs-rest linear SVM classifiers:

- Word-level TF-IDF
- Character-level TF-IDF
- Hybrid word and character TF-IDF

## Experimental Results

| Model | Coarse F1 | Fine F1 |
|---|---:|---:|
| Word TF-IDF + SVM | 0.5403 | 0.4586 |
| Character TF-IDF + SVM | 0.5514 | 0.4446 |
| Hybrid TF-IDF + SVM | 0.5543 | 0.4547 |

The evaluation uses 399 English held-out documents across three outer folds, with decision thresholds selected on inner validation data.

## Key Findings

The hybrid representation achieved the highest coarse F1 among the standard SVM models (0.5543).

For fine-grained classification, the word-based SVM achieved the best result within this group (0.4586).

## Experimental Artifacts

The original experiment archives are:

- `baseline_svm_EN_v1_foldall3_seed42_db3d1644bec1.zip`
- `baseline_svmchar_EN_v1_foldall3_seed42_f5309574ae69.zip`
- `baseline_svmhybrid_EN_v1_foldall3_seed42_ef6804790316.zip`

These archives are included in the complete project package:

[GitHub Release v1.0.0](https://github.com/Nizar-099/rare-narratives-nlp/releases/tag/v1.0.0)

After extraction, navigate to `04_Experiments/02_Standard_SVM/`.

## Additional Documentation

- [Experiment Index](../../06_Documentation/EXPERIMENT_INDEX.md)
- [Reproducibility Guide](../../06_Documentation/REPRODUCIBILITY.md)
