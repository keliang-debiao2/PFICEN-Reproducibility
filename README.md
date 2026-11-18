PFICEN Reproducibility Package
This repository contains the PFICEN implementation and supporting code for Funnel-Aware In-Context Expert Learning for Online Purchase Conversion Prediction Under Product-Domain Shift.

The package includes model source code, data-processing utilities, retrieval components, training and evaluation scripts, experiment configurations, protocol documentation, automated checks, and reference-record files. This README describes package contents without reporting experimental results.
Repository Structure
Path	Contents
src/pficen/	PFICEN model, data processing, retrieval, training, calibration, metrics, statistical utilities, and baseline components.
scripts/	Command-line entry points for data preparation and experimental workflows.
configs/	YAML configurations for prediction protocols, external evaluation, baselines, ablation, and robustness analyses.
docs/	Data schema, evaluation protocol, code mapping, anonymity notes, and reference-record provenance.
tests/	Automated checks for data construction, splits, model behavior, losses, and statistical utilities.
logs/reference_runs/	Reference log files, a manifest, and accompanying documentation.
results/reference/	CSV reference tables organized by analysis type.
pyproject.toml	Package metadata, dependencies, optional dependencies, and command-line entry-point definitions.
requirements.txt	Python dependency specifications.
environment.yml	Conda environment specification.
CITATION.cff	Citation metadata.
LICENSE	MIT license.


Model and Supporting Modules
File	Included functionality
src/pficen/model.py	Event and feature embeddings, continuous-time causal attention with funnel bias, attention pooling, context Transformer, sparse expert routing, and session-level and position-level prediction heads.
src/pficen/retrieval.py	Label-stratified FAISS retrieval, retrieval metadata, and context-selection exclusion rules.
src/pficen/losses.py	Class-balanced binary cross-entropy, retrieval consistency, funnel consistency, expert diversity, Brier loss, and combined training objectives.
src/pficen/engine.py	Model training, retrieval-index updates, encoding, and prediction routines.
src/pficen/protocols.py	Event cleaning and session-prefix construction for outcome-aligned and fifth-event protocols.
src/pficen/preprocessing.py	Categorical vocabularies and fold-specific preprocessing.
src/pficen/dataset.py	Event-prefix datasets and batch collation.
src/pficen/splits.py	User-grouped outer folds, inner user splits, chronological partitions, and user-disjointness checks.
src/pficen/io.py	Source-file discovery, event-file loading, and prepared-data loading.
src/pficen/calibration.py	Temperature scaling and F1-based classification-threshold selection.
src/pficen/metrics.py	Classification metrics, expected calibration error, and reliability-bin calculations.
src/pficen/statistics.py	Fold-summary intervals, paired bootstrap calculations, and Holm adjustment.
src/pficen/perturbations.py	Feature missingness, price perturbations, fixed-prefix construction, and training-user subsampling.
src/pficen/baselines.py	Aggregated prefix features and tabular baseline utilities.
src/pficen/neural_baselines.py	MLP, FT-Transformer, GRU/LSTM sequence components, and tabular neural fitting utilities.
src/pficen/foundation_adapters.py	Deterministic context selection and context-ensemble wrappers for externally supplied TabPFN-3 and TabFM predictor functions.
src/pficen/config.py	YAML configuration loading, configuration digests, and resolved-configuration export.
src/pficen/utils.py	Seed management, hashing, JSON writing, and batching helpers.
src/pficen/cli.py	Package command-line dispatch functions.


Workflow Scripts
Script	Purpose
scripts/prepare_data.py	Prepare event data, session prefixes, schema descriptions, construction counts, and input manifests.
scripts/run_cross_validation.py	Run the configured five-fold PFICEN training and evaluation workflow.
scripts/run_external.py	Apply a development run to external event data.
scripts/run_temporal.py	Run chronological evaluation using the fifth-event protocol.
scripts/run_baselines.py	Run aggregated-feature logistic regression, random forest, XGBoost, LightGBM, and CatBoost baselines.
scripts/run_ablation.py	Execute configured component-removal and combination variants.
scripts/run_robustness.py	Execute configured perturbation and reduced-training-data workflows.
scripts/run_statistics.py	Perform statistical summaries and comparisons from run outputs.
scripts/run_efficiency.py	Profile neural inference latency and count trainable parameters.
scripts/compare_to_reference.py	Compare generated summaries with packaged reference tables.
scripts/validate_repository.py	Check repository files and configuration consistency.
scripts/reproduce_all.py	Coordinate workflow stages in dependency order.


Configuration Files
File	Configuration scope
configs/outcome_aligned.yaml	Outcome-aligned data construction and PFICEN workflow.
configs/fifth_event.yaml	Fifth-event prefix prediction protocol.
configs/external.yaml	External evaluation for the outcome-aligned workflow.
configs/external_fifth_event.yaml	External evaluation for the fifth-event workflow.
configs/baselines.yaml	Baseline model settings.
configs/ablation.yaml	Component variants, funnel-loss sensitivity settings, and statistical-comparison settings.
configs/robustness.yaml	Feature missingness, price noise, shortened prefixes, training-user subsampling, and seed settings.


Documentation and Data Definitions
File	Contents
docs/DATA_SCHEMA.md	Public-source file selections, required event columns, ordering and filtering rules, and prepared-file definitions.
docs/PROTOCOL.md	Data-partition and evaluation-protocol documentation.
docs/METHOD_MAPPING.md	Mapping between methodological components and source files.
docs/ANONYMITY.md	Anonymity-related package notes.
docs/RESULT_PROVENANCE.md	Provenance and intended use of the packaged reference logs and tables.


The data documentation covers the REES46 multi-category-store and cosmetics-shop event sources. Raw datasets are not included. The data-preparation code defines event and session Parquet files, construction-count records, schema metadata, and preparation manifests.
Automated Checks
The tests/ directory contains checks for user-disjoint outer folds, prefix construction and purchase exclusion, model output shapes and routing, causal prefix-state behavior, funnel-loss behavior, bootstrap intervals, and Holm adjustment. Their presence documents the included checks; this README does not report execution outcomes.
Reference Files
The package contains reference logs and CSV tables covering data construction, baseline comparisons, external evaluation, calibration, ablation, robustness, funnel-loss sensitivity, and efficiency. These are manuscript-aligned reference records rather than original console logs captured during training, as documented in docs/RESULT_PROVENANCE.md. They provide comparison targets and record formats for subsequent runs.
License
The source code is distributed under the MIT license included in LICENSE.
