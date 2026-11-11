# Reproducibility Guide

## Scope

The package supports inspection of saved evidence and replay of reported metrics. Full training reproduction additionally requires original data, matching environments and the relevant training implementation. The seven notebooks do not contain every historical training workflow represented in the paper.

During package verification, all 32 ZIP archives passed member CRC checks and all seven notebooks passed format and Python syntax checks. All 28 coarse/fine Table 1 scores were recalculated from submitted predictions and archived gold labels. The original source labels were not independently reconstructed, models were not retrained, and the notebook collection was not executed end to end. Saved cell outputs remain historical records.

## Directory layout

```text
Rare_Narratives/
  README.md
  01_Report/Rare_Narratives_Research_Paper.pdf
  02_Notebooks/
  03_Setups/
  04_Experiments/
  05_Analysis/
  06_Documentation/
    EXPERIMENT_INDEX.md
    REPRODUCIBILITY.md
```

`EXPERIMENT_INDEX.md` gives exact experiment paths and prediction filenames. The following notebook filenames are the delivered versions:

| Notebook | Saved output cells / code cells | Workflow |
|---|---:|---|
| `NLP_01_Data_preparation.ipynb` | 0/8 | Source data and setup kit; validates fingerprints, taxonomy, duplicate groups, splits and metric checks. |
| `NLP_02_Exploratory_data_analysis.ipynb` | 0/12 | Source data and setup kit; descriptive tables and figures. Archived outputs are in risultati_eda.zip. |
| `NLP_03_English_baselines.ipynb` | 0/12 | Fits word TF-IDF logistic classifiers and evaluates fixed/tuned decoding. Other lexical variants have separate historical bundles. |
| `NLP_04_GPU_and_tokenizer_audit.ipynb` | 0/12 | CUDA check and pinned-tokenizer length analysis. The notebook starts with a GPU check; tokenisation itself runs on CPU. |
| `NLP_05_Transformer_preparation.ipynb` | 9/15 | Runtime, tokenisation and optional synthetic memory probes; does not implement the full fine-tuning experiments. |
| `NLP_06_Balanced_SVM_evaluation.ipynb` | 7/7 | Restores previously fitted models, verifies validation scores, evaluates outer predictions and compares systems. Does not fit the balanced SVMs from scratch. |
| `NLP_07_Multilingual_embeddings_evaluation.ipynb` | 11/12 | Restores or extracts embeddings, fits English-only and multilingual SVMs, and evaluates predictions. Historical outputs use a restored cache. |

Saved output coverage does not certify execution of the current edited source. Record fresh outputs and environment metadata for any rerun.

## Required inputs and environments

The source archives `training_NLP.zip` and `test_NLP.zip` are not included. Obtain the same releases from the original course/dataset distribution and check them against the frozen fingerprints. The test archive is used for text identity and overlap checks; test annotations are not used for the reported evaluation.

The included `03_Setups/kit_setup_nlp.zip` supplies `nlp_setup.py`, the project taxonomy, `split_manifest_v2.csv`, expected data fingerprints, duplicate-audit reference and scorer resources. `03_Setups/setup_summary.json` records preparation results; `03_Setups/experiment_config_cc51cbca204a.json` records the multilingual recipe.

Use the environment records inside each experiment bundle. Recorded runs include NumPy 2.1.3, pandas 2.3.3 and scikit-learn 1.6.1. Neural runs record PyTorch 2.11.0+cu130, Transformers 5.20.2, tokenizers 0.23.3 and Tesla T4 hardware. CPU and GPU runs have different Python/PyTorch records. These versions describe historical environments, not a newly tested installation specification or a single project lockfile.

Dependencies include NumPy, pandas, SciPy, scikit-learn, joblib, Matplotlib, PyTorch, Transformers, huggingface_hub, IPython and Jupyter. Metric replay and SVM fitting can run on CPU. The delivered embedding extraction and GPU-probe paths require CUDA. Downloading pretrained weights requires access to the pinned revisions; restoring compatible caches avoids re-extraction.

## Execution and artifact restoration

1. Select the notebook and required inputs from the table above. Each notebook reconstructs its own state; variables do not persist across notebook sessions.
2. Attach the source data, setup kit and required experiment/cache artifacts to Kaggle. Preserve the archive filenames and internal layout.
3. Configure paths before execution. Notebooks 01–03 provide `NLP_INPUT_ROOT`, `NLP_OUTPUT_ROOT`, `NLP_TRAIN_SOURCE`, `NLP_TEST_SOURCE` and `NLP_KIT_DIR` overrides. Defaults target `/kaggle/input` and `/kaggle/working/nlp_setup`. An extracted source override points to the directory containing `training/` or `test/`; a kit override points to the directory containing `nlp_setup.py`.
4. Notebook 06 uses explicit Kaggle dataset paths under `/kaggle/input/datasets/nizarmabrouk/`, including `nlp-semeval-2025-dati-e-setup` and `nlp-svm-bilanciata`. Supply equivalent mounted inputs or adjust paths in a working copy. The project directory itself does not automatically satisfy those mounts. The paired comparison additionally needs both systems' prediction artifacts.
5. For Notebook 07, select `EMBEDDING_MODE = "restore"` to use `multilingual_embeddings_be6df64d78.zip` or a compatible extracted cache. Select `"extract"` for new GPU extraction at the pinned revision. Cache restoration does not restore the fitted SVMs: subsequent training cells fit classifiers again.
6. Execute the selected notebook in order. Stop on mismatched fingerprints, label order, split membership or model-validation scores. Preserve existing experiment bundles and write new runs to distinct output directories.

The multilingual encoder is `sentence-transformers/paraphrase-multilingual-mpnet-base-v2` at revision `4328cf26390c98c5e3c738b4460a05b95f4911f5`. Its cache contains 1,688 document vectors of dimension 768. Extraction uses non-overlapping 128-token blocks including special tokens, mean pooling over non-padding states, block L2 normalisation, and a content-token-weighted mean followed by document L2 normalisation. This is the project-defined document aggregation procedure.

## Evaluation replay

The project inventory contains 22 coarse and 96 fine labels. Do not replace it with the organiser's 91-fine-label scorer inventory when reproducing the primary metric. Separately exported v3 scores use a different label projection.

The English outer folds contain 133, 134 and 132 documents. Inner training contains 213, 212 and 214 documents, respectively, with 53 validation articles per fold. Multilingual training adds 1,289 auxiliary articles. Each English document has exactly one outer prediction per system. Vocabulary estimation and classifier fitting use inner training; thresholds use inner English validation. There is no refit on training plus validation in these recipes.

To replay Table 1:

1. Locate the prediction artifact in the experiment index. Read TSV/JSON predictions or the multilingual NPZ arrays, preserving the documented label order.
2. Align by document identifier, not file row order. Require exactly 399 unique English identifiers and identical gold/prediction identifier sets. Check all predicted labels against the project taxonomy.
3. Prefer gold labels reconstructed from fingerprint-verified original data. For internal package consistency checks, the multilingual outer-evaluation NPZ provides `keys`, `gold_coarse`, `gold_fine` and the corresponding class arrays. Using those arrays does not independently validate their provenance.
4. For each level, compute `2 * |gold ∩ predicted| / (|gold| + |predicted|)` per document and take the mean over all 399 articles. Retain the support module's handling of empty sets and invalid labels. Pool documents rather than taking an unweighted mean of unequal-sized folds.
5. Compare to the four-decimal scores in the index. Preserve any discrepancy for investigation rather than overwriting historical results.

Classifiers select scores strictly above threshold and fall back to argmax when none qualify, separately per level. Thresholds remain frozen during outer evaluation. `Other` may coexist with specific labels; predicted fine labels do not necessarily imply their coarse parent.

## Statistical and support analyses

Paired bootstrap comparisons use 2,000 resamples of 395 English document groups, with the same groups sampled for both systems in each draw. Documents in a group remain together. Scores are document-weighted. Seed 20261104 is recorded for the bootstrap analyses; this is separate from classifier seed 42.

Intervals condition on saved models and fixed splits. They do not capture full retraining or split variability, all dependence from overlapping cross-validation training sets, or exploratory model-selection effects. They are marginal intervals, not equivalence tests. An interval containing zero does not establish equal performance.

Rare-label support is measured in each document's corresponding inner-training fold. Exclude global `Other` from the specific-label counts. Table 2's final row is a subset of the 1–4 band. Counts represent document-label occurrences; they must not be added across overlapping support summaries. Solver seed comparisons at fixed embeddings and splits measure solver variability only.

## Remaining evidence limits

- Original training/test source archives and a single validated environment lockfile are not included.
- The seven notebooks do not provide complete training implementations for every historical Table 1 system. Prediction replay and model restoration are distinct from training reproduction.
- The neural diagnostic bundle supports the frozen-head and gradient checks described in Section 3.2. Complete logs of earlier full-model fine-tuning and unsuccessful memorisation runs are not included; those runs are not reported as experimental evidence in the current paper.
- Several later experiments followed inspection of earlier outer errors. The study is exploratory. The separate 41 English test texts had been consulted during earlier development and are not an untouched final benchmark.
- Lexical grouping does not rule out cross-language translations or undetected paraphrases. Multilingual training changes data volume and label/domain composition as well as language.

Preserve run identifiers, model revisions, archived environments and original predictions when extending the project. New computations should retain their own provenance and should not be presented as historical executions.
