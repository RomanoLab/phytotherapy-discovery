# Phytotherapy Discovery — Ontology Work Toolkit

This repository accompanies the analysis for **“Phytotherapy Discovery through Ontology-Guided Machine Learning.”**  
It is intended to be used *with* the upstream phytotherapy ontology maintained in **RomanoLab/poppy** (the source of truth for the ontology itself):

- Upstream ontology + primary project context: https://github.com/RomanoLab/poppy

This repository also includes a modified **CTAPred** pipeline used to predict **protein–phytochemical interactions**, supporting downstream mechanism inference and repurposing analyses.

---

## Table of Contents

1. [Background](#background)
2. [Repository Layout](#repository-layout)
3. [Quick Start](#quick-start)
4. [Command-line Reference](#command-line-reference)
5. [Workflow Details](#workflow-details)
6. [Extending the Toolkit](#extending-the-toolkit)
7. [Contributing](#contributing)
8. [Citation](#citation)

---

## Background

Researchers in natural-product drug discovery often work with ontologies linking **plants → chemicals → targets → therapeutic roles**. In this project, the ontology is maintained upstream in `RomanoLab/poppy`, while this repository contains analysis companion materials and the CTAPred workflow used in the ontology-guided ML portion of the study.

At a high level, the workflow supports:

- Starting from an ontology-derived phytochemical set (from `poppy`)
- Predicting likely protein targets for phytochemicals (CTAPred)
- Using predictions for downstream analysis (e.g., candidate prioritization, mechanism inference)

---

## Repository Layout

```
.
├── README.md                    # you are here
├── requirements.txt             # repo-level environment dependencies (if applicable)
└── CTAPred/                     # modified CTAPred pipeline for protein–phytochemical predictions
    ├── predict_targets.py
    ├── SharedFunc.py
    ├── requirements.txt
    ├── QueryList1_smiles.csv
    └── README.md                # CTAPred usage instructions
```
---


```  

| File / Dir             | Purpose                                                                      |
| ---------------------- | -----------------------------------------------------------------------------|
| `CTAPred/`             | Modified CTAPred pipeline used to predict protein–phytochemical interactions |
| `CTAPred/README.md     | Canonical usage instructions for running CTAPred in this repo                |
| `Crequirements.txt`    | Repo-level dependencies used by analysis utilities                           |

```
---

## Quick Start

### 1. Clone

    git clone https://github.com/RomanoLab/phytotherapy-discovery.git
    cd phytotherapy-discovery

### 2. (Recommended) Create a virtual environment

    python -m venv .venv
    source .venv/bin/activate      # Windows: .venv\Scripts\activate

### 3. Install dependencies

If you are running CTAPred, install CTAPred’s pinned dependencies:

    pip install -r CTAPred/requirements.txt

If you are running other repo-level analysis utilities, you may also install the root requirements:

    pip install -r requirements.txt

### 4. Run CTAPred

Follow the instructions in `CTAPred/README.md`. To see the CLI options:

    python CTAPred/predict_targets.py --help

`CTAPred/QueryList1_smiles.csv` is provided as an example/input artifact containing phytochemical SMILES used for predictions.

---

## Command-line Reference

Because this repository’s executable workflow is centered on CTAPred, the authoritative CLI reference is:

    python CTAPred/predict_targets.py --help

For usage examples, input expectations, and output files, see:

- `CTAPred/README.md`

---

## Workflow Details
A typical end-to-end workflow looks like this:
1) Consult / generate ontology artifacts upstream
Use RomanoLab/poppy to access the ontology and (if needed) derive a phytochemical set for ML analysis.
2) Prepare CTAPred inputs
Provide a CSV of phytochemical SMILES (use CTAPred/QueryList1_smiles.csv as a template).
3) Run CTAPred predictions
Execute CTAPred/predict_targets.py to generate predicted protein targets / ranked interactions.
4) Downstream analysis / integration
Use predictions for prioritization, hypothesis generation, or reintegration into ontology/KG analyses (depending on your study design and tooling).

---

## Extending the Toolkit
Ideas that keep this repository aligned with its current scope:
* **Modularise** – split into smaller modules and expose a proper Python API.
* **Unit tests** – add `pytest` and GitHub Actions for continuous integration.
* **Visualisation** – integrate network diagrams or heatmaps (e.g., via `matplotlib`).
* **Docker** – package the pipeline for reproducible runs on any machine.

---

## Contributing
1. Fork → create a feature branch → commit + push → open a Pull Request.
2. Keep changes scoped and well-described (what/why/how).
3. If you change model inputs/outputs, update CTAPred/README.md and this README accordingly.

---

## Citation
If you use this repository in research, please cite:

```bibtex
@software{hewryk_ontology_work_2025,
  author       = {Hewryk, Oresta S. I. and Pan, Ian Tong and Romano, Joseph D.},
  title        = {{Ontology Work}: A Python toolkit for phytotherapy ontology enrichment},
  year         = {2025},
  publisher    = {GitHub},
  url          = {https://github.com/RomanoLab/ontology-work}
}
```



