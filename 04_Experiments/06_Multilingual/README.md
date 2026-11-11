# Multilingual Experiments — Rare Narrative Classification

This directory documents the multilingual experiments conducted for rare narrative classification in news articles.

## Overview

One of the main challenges in narrative classification is the limited number of training examples available for rare labels.

The multilingual experiments investigate whether incorporating training data from multiple languages can improve the recognition of underrepresented narrative categories.

The objective is to assess the potential benefits of multilingual training while examining its impact on classification performance in English news.

## Experimental Objectives

The experiments focus on:

- Investigating multilingual training as an approach to improve rare narrative recognition.
- Comparing multilingual configurations with English-only baselines.
- Evaluating classification performance on coarse and fine narrative labels.
- Examining the trade-off between overall predictive performance and the recognition of less frequent labels.

## Key Findings

The multilingual experiments revealed an important trade-off.

Although incorporating multilingual training data helped recover some rare narrative labels, it did not produce an overall improvement in classification performance compared with the strongest English-only models.

These findings suggest that increasing training-data diversity does not necessarily improve aggregate performance, but may still provide benefits for categories with limited representation.

The detailed experimental results and label-level analyses are available in the project documentation and archived outputs.

## Experimental Artifacts

The original experiment outputs, configurations and evaluation results are included in the complete project archive.

[GitHub Release v1.0.0](https://github.com/Nizar-099/rare-narratives-nlp/releases/tag/v1.0.0)

After downloading and extracting `Rare_Narratives.rar`, navigate to:

`04_Experiments/06_Multilingual/`

## Additional Documentation

- [Experiment Index](../../06_Documentation/EXPERIMENT_INDEX.md)
- [Reproducibility Guide](../../06_Documentation/REPRODUCIBILITY.md)

The experiment index provides the correspondence between evaluated configurations, reported results and archived experimental artifacts.
