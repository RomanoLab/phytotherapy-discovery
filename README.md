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

```text
.
├── README.md                    # you are here
├── requirements.txt             # repo-level environment dependencies (if applicable)
└── CTAPred/                     # modified CTAPred pipeline for protein–phytochemical predictions
    ├── predict_targets.py
    ├── SharedFunc.py
    ├── requirements.txt
    ├── QueryList1_smiles.csv
    └── README.md                # CTAPred usage instructions
File / Dir	Purpose
CTAPred/	Modified CTAPred pipeline used to predict protein–phytochemical interactions
CTAPred/README.md	Canonical usage instructions for running CTAPred in this repo
requirements.txt	Repo-level dependencies used by analysis utilities / notebooks (if applicable)

Quick Start
1) Clone
bash
Copy code
git clone https://github.com/RomanoLab/phytotherapy-discovery.git
cd phytotherapy-discovery
2) (Recommended) Create a virtual environment
bash
Copy code
python -m venv .venv
source .venv/bin/activate     # Windows: .venv\Scripts\activate
3) Install dependencies
If you are running CTAPred, install CTAPred’s pinned dependencies:

bash
Copy code
pip install -r CTAPred/requirements.txt
If you are running other repo-level analysis utilities, you may also install the root requirements:

bash
Copy code
pip install -r requirements.txt
4) Run CTAPred
Follow the instructions in CTAPred/README.md. To see the CLI options:

bash
Copy code
python CTAPred/predict_targets.py --help
CTAPred/QueryList1_smiles.csv is provided as an example/input artifact containing phytochemical SMILES used for predictions.

Command-line Reference
Because this repository’s executable workflow is centered on CTAPred, the authoritative CLI reference is:

bash
Copy code
python CTAPred/predict_targets.py --help
For usage examples, input expectations, and output files, see:

CTAPred/README.md

Workflow Details
A typical end-to-end workflow looks like this:

Consult / generate ontology artifacts upstream
Use RomanoLab/poppy to access the ontology and (if needed) derive a phytochemical set for ML analysis.

Prepare CTAPred inputs
Provide a CSV of phytochemical SMILES (use CTAPred/QueryList1_smiles.csv as a template).

Run CTAPred predictions
Execute CTAPred/predict_targets.py to generate predicted protein targets / ranked interactions.

Downstream analysis / integration
Use predictions for prioritization, hypothesis generation, or reintegration into ontology/KG analyses (depending on your study design and tooling).

Extending the Toolkit
Ideas that keep this repository aligned with its current scope:

Make CTAPred outputs easier to consume (standardize output schemas; add converters to KG/CSV/Parquet).

Add reproducibility tooling (Dockerfile; pinned Python versions; small test fixtures).

Add CI (lint + unit tests for CTAPred helper functions; smoke test on sample inputs).

Add analysis notebooks that explicitly document how CTAPred outputs connect back to the upstream ontology.

Contributing
Fork → create a feature branch → commit + push → open a Pull Request.

Keep changes scoped and well-described (what/why/how).

If you change model inputs/outputs, update CTAPred/README.md and this README accordingly.

Citation
If you use this repository in research, please cite:

bibtex
Copy code
@software{romanolab_phytotherapy_discovery_2025,
  author       = {Hewryk, Oresta S. I. and Pan, Ian Tong and Romano, Joseph D.},
  title        = {{phytotherapy-discovery}: Ontology-guided phytochemical discovery utilities and CTAPred workflow},
  year         = {2025},
  publisher    = {GitHub},
  url          = {https://github.com/RomanoLab/phytotherapy-discovery}
}
makefile
Copy code
::contentReference[oaicite:0]{index=0}




# Ontology Work Toolkit

This is the analysis for "Phytotherapy Discovery through Ontology-Guided Machine Learning" in which we use the ontology found at https://github.com/RomanoLab/poppy. Please consult the aformentioned repository first before embarking on the analysis.

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

Researchers in natural-product drug discovery often work with sprawling ontologies that link **plants → chemicals → targets → therapeutic roles**. The original notebook captured a proof-of-concept pipeline for:

* Parsing large OWL/Turtle files
* Adding computed fingerprints (ECFP) from a CSV
* Running SPARQL metrics queries
* Exporting summary statistics for publication figures

This repository converts that exploratory notebook into **clean, script-first code** that can be version-controlled, tested, and deployed.

---

## Repository Layout

```
.
├── src/
│   └── ontology_work.py        # main script (refactored notebook code)
├── data/                       # ontologies / CSVs here 
├── requirements.txt            # pinned dependencies for SRC.py
├── CTAPred/  
│   └── predict_targets.py      # CTAPred pipeline drivers script
│   └── SharedFunc.py           # CTApred helper functions
│   └── requirements.txt        # dependencies for CTAPred pipeline
│   └── QueryList1_smiles.csv   # CTAPred input containing all phytochemicals
│   └── README.md               # instructions for using the CTAPred pipeline
└── README.md                   # you are here
```  

| File / Dir             | Purpose                                                     |
| ---------------------- | ----------------------------------------------------------- |
| `SRC.py`               | Entry-point that orchestrates parsing, enrichment & metrics |
| `data/`                | Placeholder for ontology TTL/RDF files and CSV inputs       |
| `requirements.txt`     | Packages required to run ontology workflow                  |
| `CTAPred/`             | Modified CTAPred pipeline for predicting protein-phytochemical interactions |


---

## Quick Start

1. **Clone & install**

   ```bash
   git clone https://github.com/<your-org>/ontology-work.git
   cd ontology-work
   python -m venv .venv          # optional but recommended
   source .venv/bin/activate     # Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   ```

2. **Run the script**

   ```bash
   python -m src.ontology_work \
         --ontology data/phytotherapies.ttl \
         --ecfp-csv data/phytotherapy_ecfp.csv \
         --out metrics.json
   ```

   Results:

   * `metrics.json` – counts of classes, individuals, triples, etc.
   * `phytotherapies_enriched.ttl` – copy of the ontology with `hasECFP` data properties inserted.

---

## Command-line Reference

```text
usage: ontology_work.py [-h] --ontology PATH [--ecfp-csv PATH]
                        [--out PATH] [--log-level {DEBUG,INFO,WARNING,ERROR}]

optional arguments:
  --ontology PATH      input OWL/Turtle/RDF file (required)
  --ecfp-csv PATH      CSV with columns `smiles,ecfp` for enrichment
  --out PATH           where to save metrics JSON (default: stdout)
  --log-level LEVEL    set log verbosity (default: INFO)
```

---

## Workflow Details

1. **Parse ontology** using **rdflib** – handles TTL, RDF/XML, OWL.
2. **Compute / insert fingerprints** – matches individuals by `hasSmiles` and adds `hasECFP`.
3. **SPARQL metrics** – counts classes, properties, individuals, & custom queries.
4. **Export artifacts** – enriched TTL plus JSON metrics for figures or dashboards.

---

## Extending the Toolkit

* **Modularise** – split into smaller modules and expose a proper Python API.
* **Unit tests** – add `pytest` and GitHub Actions for continuous integration.
* **Visualisation** – integrate network diagrams or heatmaps (e.g., via `matplotlib`).
* **Docker** – package the pipeline for reproducible runs on any machine.

---

## Contributing

1. Fork → feature branch → commit + push → Pull Request.
2. Follow [PEP 8](https://peps.python.org/pep-0008/) and add/ update tests.
3. Be descriptive in PR titles & commit messages.

---

## Citation

If you use this code in your research, please cite:

```bibtex
@software{hewryk_ontology_work_2025,
  author       = {Hewryk, Oresta S. I. and Pan, Ian Tong and Romano, Joseph D.},
  title        = {{Ontology Work}: A Python toolkit for phytotherapy ontology enrichment},
  year         = {2025},
  publisher    = {GitHub},
  url          = {https://github.com/RomanoLab/ontology-work}
}
```

