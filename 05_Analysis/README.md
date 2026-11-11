# Analysis — Experimental Evaluation and Interpretation

This directory documents the analyses conducted to evaluate and interpret the results of the rare narrative classification project.

## Overview

Beyond comparing overall classification scores, the project investigates how different models behave across narrative categories, particularly those with limited training examples.

The analyses support the interpretation of the experimental findings presented in the research paper.

## Main Analysis Areas

### Exploratory Data Analysis

Examination of the dataset, narrative-label distributions and class imbalance, with particular attention to underrepresented categories.

### Model Evaluation

Comparison of classification performance across the evaluated models, considering both coarse-grained and fine-grained narrative labels.

### Statistical Analysis

Statistical comparisons and uncertainty assessments used to support the interpretation of experimental results.

### Qualitative Analysis

Investigation of classification errors and individual narrative categories to better understand model strengths and limitations.

### Tokenization and Feature Analysis

Examination of the lexical and representation-related aspects of the experimental pipeline.

## Key Findings

The analyses provide additional context for the main findings:

- Lexical representations remain competitive for narrative classification.
- Balanced Word SVM achieved a Fine F1 of 0.4617.
- Combining word-level TF-IDF and MPNet representations achieved a Coarse F1 of 0.5598.
- Multilingual training helped recover some rare narrative labels but did not improve overall performance compared with the strongest English-only configurations.

These findings should be interpreted alongside the experimental methodology, label-level results and evaluation limitations discussed in the research paper.

## Analysis Artifacts

The complete original analysis outputs are included in the full project archive.

[GitHub Release v1.0.0](https://github.com/Nizar-099/rare-narratives-nlp/releases/tag/v1.0.0)

After extracting `Rare_Narratives.rar`, navigate to:

`05_Analysis/`

## Additional Documentation

- [Experiment Index](../06_Documentation/EXPERIMENT_INDEX.md)
- [Reproducibility Guide](../06_Documentation/REPRODUCIBILITY.md)

Refer to these documents and the research paper for the exact correspondence between experimental results, analyses and archived artifacts.
