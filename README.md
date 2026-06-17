# Repository Structure & Component Guide

```
network-ai-workspace/
├── configs/              # Centralized hyperparameter & environment configurations
├── data/                 # Data warehouse (Raw NetSim logs to processed ML tensors)
├── models/               # Serialized model checkpoints (.pkl, .h5, saved_model)
├── reports/              # Performance metrics, evaluation tables, and figures
├── notebooks/            # Sandboxed prototyping & exploratory data analysis (EDA)
├── src/                  # Production-ready, modular core source code
└── scripts/              # Automation entry points for pipelines and training

```

---

### 📂 Root Workspace Files

* **`README.md`** — Main repository documentation containing project architecture, setup instructions, and execution workflows.
* **`requirements.txt`** — Monolithic list of Python dependencies required to run both network intelligence pipelines.
* **`.gitignore`** — Prevents heavy serialized models, untracked raw data files, and local IDE metadata from hitting version control.
* **`.env.example`** — Template for environment variables, defining system-specific paths to local NetSim installations and binaries.

### 📂 `configs/` — Unified Engine Parameters

* **`configs/common.yaml`** — Shared global configurations, pipeline random seeds, logging levels, and unified export targets.
* **`configs/netsim.yaml`** — NetSim simulation specific parameters, layout topologies, application settings, and sampling intervals.
* **`configs/netfault_diagnosis.yaml`** — Multi-class model definitions, training hyper-parameters, layer boundaries, and evaluation splits for Engine 1.
* **`configs/netanom_detection.yaml`** — Sliding window sizes, compression bounds, and reconstruction loss targets for Engine 2.

### 📂 `data/` — Isolated Data Pipelines

* **`data/raw/netsim_exports/`** — Immutable directory storing unparsed pcap files, raw device status logs, and traffic tables straight from NetSim.
* **`data/interim/`** — Middle-tier structured data storage where raw NetSim report files are unified into cleaned, row-oriented formats.
* **`data/processed/netfault_diagnosis/`** — Final feature-engineered static snapshots (`.csv`) and temporal sequence matrices (`.npy`) for fault classification.
* **`data/processed/netanom_detection/`** — Chronologically sequenced normal behavioral baselines and windowed attack sequences for anomaly detection.

### 📂 `models/` — Serialized Model Registry

* **`models/netfault_diagnosis/`** — Production weights, pipeline transformers, and picking files for classical tree classifiers and LSTM models.
* **`models/netanom_detection/`** — Saved model architectures and learned weight matrices for dense/convolutional Autoencoders and Isolation Forests.

### 📂 `reports/` — Analytics & Artifacts

* **`reports/figures/`** — Saved confusion matrices, ROC curves, loss trajectories, and SHAP/feature attribution plots.
* **`reports/tables/`** — Markdown and LaTeX tables comparing structural model performance metrics across engines.
* **`reports/metrics/`** — JSON structured evaluation dumps tracking model precision, recall, F1-scores, and wall-clock inference latencies.

### 📂 `notebooks/` — Development Sandboxes

* **`01_netsim_exploration.ipynb`** — Interactive parsing, parsing validation, and initial structural analysis of raw NetSim outputs.
* **`02_shared_feature_analysis.ipynb`** — Feature prototyping (e.g., assessing routing loops numerically and validating traffic delta signals).
* **`03_netfault_diagnosis.ipynb`** — Prototyping multi-class fault classification, comparing traditional ensemble trees against Keras sequence models.
* **`04_netanom_detection.ipynb`** — Establishing unsupervised baselines, testing reconstruction error bounds, and profiling autoencoders.
* **`05_final_comparison.ipynb`** — Monolithic evaluation notebook visualizing cross-engine capability and summarizing overall platform efficacy.

### 📂 `src/` — Modular Core System Source

* **`src/common/netsim_exporter.py`** — Wrapper utility to scrub, format, and ingestion-proof tabular raw metrics from local NetSim directories.
* **`src/common/data_utils.py`** — Core backend functions managing file I/O operations, cross-validation splits, and tensor reshaping.
* **`src/common/feature_engineering.py`** — Mathematical pipeline generating complex features like packet-delivery ratios, loop indicators, and load deltas.
* **`src/common/visualizer.py`** — Centralized charting engine standardized for plotting live telemetry, anomaly boundaries, and training diagnostics.
* **`src/common/config.py`** — Strongly-typed Python configuration management framework mapping YAML settings into internal model components.
* **`src/netfault_diagnosis/`** — End-to-end modular components for state-snapshot building, classical/DL training routines, and classification scoring.
* **`src/netanom_detection/`** — End-to-end unsupervised pipeline components for sequence-window building, autoencoder architectures, and dynamic threshold tuning.

### 📂 `scripts/` — Execution & Automation Layer

* **`scripts/run_netfault_diagnosis_pipeline.py`** — Orchestration script executing raw-to-processed pipelines for structural fault logging.
* **`scripts/run_netanom_detection_pipeline.py`** — Orchestration script generating continuous baseline traffic frames and windowed attack models.
* **`scripts/train_netfault_diagnosis_models.py`** — Fits, cross-validates, evaluates, and serializes classical and deep learning fault engines.
* **`scripts/train_netanom_detection_models.py`** — Compresses normal baseline matrices to tune autoencoder models and threshold parameters.
* **`scripts/compare_all_results.py`** — Aggregates evaluations from both system engines to output unified cross-architecture runtime performance tables.

### 📂 `tests/` — Test Suite

* **`tests/test_feature_engineering.py`** — Unit tests validating mathematical boundary constraints for engineered network features.
* **`tests/test_netsim_exporter.py`** — Verifies parsing resiliency and schema validation against breaking changes in simulator outputs.
* **`tests/test_netfault_diagnosis_pipeline.py`** — Integration test mapping step-by-step functionality from fault generation to diagnostic inference.
* **`tests/test_netanom_detection_pipeline.py`** — Integration test verifying window generation mechanics and dynamic threshold convergence.