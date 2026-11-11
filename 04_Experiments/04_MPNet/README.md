# MPNet — Semantic Document Embeddings

This directory documents the experiments based on MPNet document embeddings for multilabel narrative classification in English news.

## Overview

The objective of these experiments is to investigate whether semantic document representations can improve narrative classification compared with traditional lexical features.

Unlike TF-IDF, which represents documents through word and character frequencies, MPNet embeddings capture contextual and semantic information from the article text.

## Experimental Approaches

The experiments explore:

- **Semantic representations:** Using MPNet embeddings as document-level features.
- **Lexical and semantic features:** Combining MPNet embeddings with TF-IDF representations.
- **Performance comparison:** Evaluating the different feature representations on coarse and fine narrative classification.
- **Rare narrative analysis:** Investigating the behavior of semantic features on less frequent narrative categories.

## Evaluation

The corresponding experimental outputs provide the evaluation results and configurations used in the research paper.

For exact performance values and the mapping between experiments and reported results, consult the experiment index.

## Experimental Artifacts

The complete experimental outputs are included in the project archive:

[Download the complete project — Release v1.0.0](https://github.com/Nizar-099/rare-narratives-nlp/releases/tag/v1.0.0)

After extraction, navigate to:

`04_Experiments/04_MPNet/`

## Additional Documentation

- [Experiment Index](../../06_Documentation/EXPERIMENT_INDEX.md)
- [Reproducibility Guide](../../06_Documentation/REPRODUCIBILITY.md)
