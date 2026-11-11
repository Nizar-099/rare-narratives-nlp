# Rare Narrative Recognition in English News

This project studies multilabel narrative classification on SemEval-2025 Task 10, Subtask 2. It compares lexical classifiers, frozen document embeddings, class weighting and multilingual training, with particular attention to rare fine-grained labels.

## Contents

| Directory | Contents |
|---|---|
| `01_Report/` | Five-page research paper |
| `02_Notebooks/` | Seven notebooks for preparation, analysis and selected experimental workflows |
| `03_Setups/` | Frozen setup kit, preparation summary and multilingual configuration |
| `04_Experiments/` | Training artifacts, embedding caches and evaluation bundles by model family |
| `05_Analysis/` | Data analyses, evaluation outputs, statistical comparisons and qualitative cases |
| `06_Documentation/` | Experiment index and reproduction requirements |

Start with [the research paper](01_Report/Rare_Narratives_Research_Paper.pdf), then use the [experiment index](06_Documentation/EXPERIMENT_INDEX.md) to locate its supporting predictions. The [reproducibility guide](06_Documentation/REPRODUCIBILITY.md) distinguishes inspection, evaluation replay and training from source.

## Protocol and findings

Evaluation pools one outer-fold prediction for each of 399 English articles across three fixed grouped folds. Thresholds are selected on inner English validation. The primary metric is document-averaged fine-label F1 under the project inventory of 22 coarse and 96 fine labels.

The balanced word SVM achieved the highest observed fine F1 (0.4617). Combining word features with full-article English MPNet embeddings achieved the highest coarse F1 (0.5598). Auxiliary-language training recovered more annotations in several rare-label groups but did not improve overall document F1 relative to English-only training with the same multilingual encoder. These comparisons are exploratory; observed rankings do not establish statistically reliable superiority.

## Verification and reproduction

The 32 included ZIP archives passed member CRC checks. All 14 Table 1 systems were recalculated from saved predictions and archived gold-label arrays, reproducing the paper's coarse and fine scores to four decimals. This confirms internal numerical consistency; it does not establish fresh training or independently validate labels against the original data release.

The seven notebooks passed format and Python syntax checks. Saved outputs are historical execution records; the delivered collection was not run end to end during package verification. Not all model-training workflows are included. The source archives `training_NLP.zip` and `test_NLP.zip` must be obtained separately from the original distribution. Runtime, artifact and evidence limitations are detailed in the reproducibility guide.
