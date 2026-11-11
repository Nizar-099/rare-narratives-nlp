# Experiment Index

All paths below are relative to the `Rare_Narratives/` project root. A path followed by an arrow identifies a member inside a ZIP archive. Experiment archive names retain their original run identifiers.

## Paper Table 1: evaluation evidence

The table maps each reported system to its saved outer predictions. All scores were recalculated using the archived gold-label matrices, aligned by English document identifier, and match the paper to four decimals. Each system covers the same 399 unique articles. The primary inventory contains 22 coarse and 96 fine labels.

| System | Coarse F1 | Fine F1 | Prediction artifact |
|---|---:|---:|---|
| Always Other | .4236 | .4236 | `04_Experiments/05_Balanced_SVM/svmbal_EN_v1_seed42_0f15a800d0.zip` → `Other_constant_predictions.json` |
| Word TF-IDF + logistic regression | .4731 | .4282 | `04_Experiments/01_Logistic_Regression/baseline_EN_v1_foldall3_seed42_295db0632ddb.zip` → `TFIDF_threshold_tuned_out_of_fold.tsv` |
| Character TF-IDF + logistic regression | .4670 | .4252 | `04_Experiments/01_Logistic_Regression/baseline_char_EN_v1_foldall3_seed42_d4e10a56178d.zip` → `TFIDF_char_threshold_tuned_out_of_fold.tsv` |
| Word + character TF-IDF + logistic regression | .4782 | .4233 | `04_Experiments/01_Logistic_Regression/baseline_hybrid_EN_v1_foldall3_seed42_298ffe0ee938.zip` → `TFIDF_hybrid_threshold_tuned_out_of_fold.tsv` |
| Frozen mBERT + linear head | .4724 | .3929 | `04_Experiments/03_Transformers/mBERT_frozen_EN_v1_seed42_01dd41dbe1.zip` → `outer_predictions.json` |
| Word TF-IDF + SVM | .5403 | .4586 | `04_Experiments/02_Standard_SVM/baseline_svm_EN_v1_foldall3_seed42_db3d1644bec1.zip` → `TFIDF_word_SVM_threshold_tuned_out_of_fold.tsv` |
| Character TF-IDF + SVM | .5514 | .4446 | `04_Experiments/02_Standard_SVM/baseline_svmchar_EN_v1_foldall3_seed42_f5309574ae69.zip` → `TFIDF_char_SVM_threshold_tuned_out_of_fold.tsv` |
| Word + character TF-IDF + SVM | .5543 | .4547 | `04_Experiments/02_Standard_SVM/baseline_svmhybrid_EN_v1_foldall3_seed42_ef6804790316.zip` → `TFIDF_hybrid_SVM_threshold_tuned_out_of_fold.tsv` |
| English MPNet, first block + SVM | .5090 | .4305 | `05_Analysis/02_Model_Evaluation/evaluation_0de7ee8579.zip` → `MPNet_first_chunk_SVM_tuned_predictions.json` |
| English MPNet, full article + SVM | .5434 | .4550 | `05_Analysis/02_Model_Evaluation/evaluation_0de7ee8579.zip` → `MPNet_all_chunks_SVM_tuned_predictions.json` |
| Word TF-IDF + full English MPNet + SVM | .5598 | .4572 | `05_Analysis/02_Model_Evaluation/evaluation_22515d4884.zip` → `TFIDF_MPNet_SVM_tuned_predictions.json` |
| Word TF-IDF + balanced SVM | .5498 | .4617 | `04_Experiments/05_Balanced_SVM/svmbal_EN_v1_seed42_0f15a800d0.zip` → `TFIDF_word_SVM_balanced_threshold_tuned_predictions.json` |
| Multilingual encoder + SVM, English training | .5417 | .4407 | `04_Experiments/06_Multilingual/multilingual_SVM_EN_vs_MULTI_seed42_35e21ad56f_outer_evaluation.npz` |
| Multilingual encoder + SVM, five-language training | .5272 | .4326 | `04_Experiments/06_Multilingual/multilingual_SVM_EN_vs_MULTI_seed42_35e21ad56f_outer_evaluation.npz` |

In the multilingual NPZ, `keys` and `fold` identify articles and partitions. `gold_coarse`, `gold_fine`, `classes_coarse` and `classes_fine` define targets and class order. The English-only predictions are `EN_only_coarse` and `EN_only_fine`; the five-language predictions are `EN_plus_auxiliary_coarse` and `EN_plus_auxiliary_fine`.

The TSV prediction files have no header: document identifier, semicolon-separated coarse labels, and semicolon-separated fine labels. JSON prediction records contain label lists and identifiers (`id` or `document_id`, depending on the experiment).

## Training and representation artifacts

Lexical logistic-regression and standard-SVM bundles listed above also preserve fitted models and validation artifacts. The following bundles complement the separate evaluation files:

- **English MPNet cache:** `04_Experiments/04_MPNet/mpnet_EN_fa59581aca.zip`.
- **English MPNet SVMs, first and full article:** `04_Experiments/04_MPNet/mpnet_SVM_EN_v1_foldall3_seed42_5ce9e43ba97c.zip`.
- **Word features plus English MPNet SVMs:** `04_Experiments/04_MPNet/TFIDF_MPNet_SVM_EN_v1_foldall3_seed42_342355099a5d.zip`.
- **Balanced word SVM training:** `04_Experiments/05_Balanced_SVM/baseline_svmbal_EN_v1_foldall3_seed42_b95ee10b0ccd_training.zip`.
- **Multilingual embedding cache:** `04_Experiments/06_Multilingual/multilingual_embeddings_be6df64d78.zip`.
- **English-only and multilingual SVM training:** `04_Experiments/06_Multilingual/multilingual_SVM_EN_vs_MULTI_seed42_35e21ad56f.zip`.

### Frozen mBERT

- `04_Experiments/03_Transformers/mBERT_frozen_EN_v1_fold1_seed42_f86c77bcfa.zip`.
- `04_Experiments/03_Transformers/mBERT_frozen_EN_v1_fold2_seed42_78476c454e.zip`.
- `04_Experiments/03_Transformers/mBERT_frozen_EN_v1_fold3_seed42_5f366a506c.zip`.

The archived recipe uses `google-bert/bert-base-multilingual-cased` at revision `3f076fdb1ab68d5b2880cb87a0886f315b8146f8`, with frozen encoder parameters, evaluation mode, FP16 autocast and 512-token right truncation. The unnormalised 768-dimensional `pooler_output` feeds a float32 linear head with 118 outputs. The head is fitted on CPU with full-inner-training batches, mean binary cross-entropy over outputs, AdamW at 0.01, zero weight decay and no dropout. Validation occurs every 50 updates, up to 1,000 updates. The best inner-validation fine document F1 selects the checkpoint; ties select the earlier update. Separate coarse/fine thresholds are selected on validation. Per-fold configurations and histories are in the listed bundles.

## Supporting analyses

- **Data exploration:** `05_Analysis/01_Data_Analysis/risultati_eda.zip`.
- **Multilingual training support:** `05_Analysis/01_Data_Analysis/support_audit_4536f2704d.zip`.
- **Error analysis by training support:** `05_Analysis/01_Data_Analysis/training_support_seed42_26e46c5637.zip`.
- **Aligned lexical and semantic predictions:** `05_Analysis/01_Data_Analysis/aligned_seed42_1e3bc98960.zip`.
- **Lexical and semantic paired bootstrap:** `05_Analysis/03_Statistical_Tests/bootstrap_seed42_2d8042d81b.zip`.
- **Balanced versus original SVM comparison:** `04_Experiments/05_Balanced_SVM/svm_balancing_seed42_ea06fb6e82.zip`.
- **Descriptive error analysis:** `05_Analysis/02_Model_Evaluation/descriptive_seed42_e59005f96e.zip`.
- **Validation-only decoding comparisons:** `05_Analysis/02_Model_Evaluation/validation_v1_4b2ee49c54.zip`.
- **Selected qualitative cases:** `05_Analysis/04_Qualitative_Analysis/qualitative_seed42_ba4d0e5d7e.zip` → `casi_da_leggere.md`.
- **Tokenizer audit:** `05_Analysis/05_Tokenizer_Audit/tokenizer_audit.zip`.
- **Transformer preparation:** `04_Experiments/03_Transformers/preparazione_transformer.zip`.
- **Frozen-head and gradient diagnostics:** `04_Experiments/03_Transformers/diagnostiche_transformer.zip`.

### Multilingual supplementary results

- **Paired bootstrap intervals:** `04_Experiments/06_Multilingual/multilingual_SVM_EN_vs_MULTI_seed42_35e21ad56f_bootstrap_appaiato.csv`.
- **Fixed-zero-threshold sensitivity:** `04_Experiments/06_Multilingual/multilingual_SVM_EN_vs_MULTI_seed42_35e21ad56f_fixed_threshold.csv`.
- **Table 2 support-band counts:** `04_Experiments/06_Multilingual/multilingual_SVM_EN_vs_MULTI_seed42_35e21ad56f_rare_labels.csv`.
- **Solver seed comparison:** `04_Experiments/06_Multilingual/multilingual_SVM_EN_vs_MULTI_seed42_35e21ad56f_solver_seeds.csv`.

The rare-label and bootstrap CSVs agree with the corresponding paper tables and intervals. This consistency check did not independently rerun either analysis. The last rare-label row is a subset of the 1–4 support band, not an additional disjoint category.

## Notebook coverage

- `02_Notebooks/NLP_01_Data_preparation.ipynb`.
- `02_Notebooks/NLP_02_Exploratory_data_analysis.ipynb`.
- `02_Notebooks/NLP_03_English_baselines.ipynb`.
- `02_Notebooks/NLP_04_GPU_and_tokenizer_audit.ipynb`.
- `02_Notebooks/NLP_05_Transformer_preparation.ipynb`.
- `02_Notebooks/NLP_06_Balanced_SVM_evaluation.ipynb`.
- `02_Notebooks/NLP_07_Multilingual_embeddings_evaluation.ipynb`.

The notebook-specific inputs and execution coverage are described in `REPRODUCIBILITY.md`. Notebook 05 covers runtime, tokenisation and memory preparation. Section 3.2 of the paper describes the archived frozen-head diagnostic and gradient audit, followed by the separate three-fold frozen-mBERT evaluation. Earlier full-model fine-tuning and unsuccessful memorisation runs are not reported as experimental evidence in the current paper; their complete logs are not included.
