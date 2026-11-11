# Balanced SVM — Class Imbalance Experiments

This directory documents the experiments investigating class imbalance in multilabel narrative classification.

## Overview

The dataset contains narrative categories with substantially different frequencies. This makes classification particularly challenging for rare narratives, as models may favor frequently represented labels.

The Balanced SVM experiments investigate approaches to address this problem while maintaining the evaluation methodology used throughout the project.

## Experimental Objectives

The main objectives are:

- Investigating the impact of class imbalance on narrative classification.
- Comparing balanced SVM configurations with standard lexical baselines.
- Evaluating performance separately for coarse and fine-grained narrative labels.
- Examining the ability of the models to recognize less frequent narrative categories.

## Key Findings

The Balanced Word SVM achieved a fine-grained F1 score of **0.4617**, representing the highest fine F1 among the evaluated systems reported in the research paper.

This result highlights the relevance of addressing class imbalance when working with fine-grained narrative categories.

However, the overall score does not fully describe performance on individual rare labels. The accompanying analyses provide additional context for interpreting these results.

## Experimental Artifacts

The original experiment outputs and configurations are included in the complete project archive.

[GitHub Release v1.0.0](https://github.com/Nizar-099/rare-narratives-nlp/releases/tag/v1.0.0)

After extracting `Rare_Narratives.rar`, navigate to:

`04_Experiments/05_Balanced_SVM/`

## Additional Documentation

- [Experiment Index](../../06_Documentation/EXPERIMENT_INDEX.md)
- [Reproducibility Guide](../../06_Documentation/REPRODUCIBILITY.md)

The experiment index provides the correspondence between model configurations, reported results and archived artifacts.
