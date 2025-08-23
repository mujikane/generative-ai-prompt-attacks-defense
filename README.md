# generative-ai-prompt-attacks-defense

Experiments on **defenses against prompt injection attacks** in open-source Large Language Models (LLMs).  
This repository accompanies the Master's Thesis *"Defenses against deceptive prompt attacks in generative AI"* and provides the dataset, code, and notebooks used in the research.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/<usuario>/generative-ai-prompt-attacks-defense)

---

## 📂 Repository structure

- `data/`
  - `dataset.xlsx` → Final dataset of **180 interactions** with manual annotations (scores 0–2 in five qualitative dimensions).
- `notebooks/`
  - `01_create_dataset.ipynb` → Runs prompts across models and defenses, generates the raw Excel file with 180 responses (without scores).
  - `02_descriptive_analysis.ipynb` → Loads the manually annotated Excel (`dataset.xlsx`) and performs descriptive and quantitative analysis.
  - `03_additional_experiment.ipynb` → Extra experiment (appendix, not part of the main thesis).
- `src/`
  - `defenses.py` → Input filtering and prompt shielding implementations.
  - `analysis.py` → Helper functions for loading the dataset and computing metrics.
  - `run_experiment.py` → Skeleton for running prompt–model–defense combinations.
- `results/`
  - `tablas/` → Aggregated results (CSV/XLSX).
  - `figuras/` → Plots (PNG/PDF).

---

## 🧪 Workflow

There are two possible ways to reproduce the results:

1. **Full pipeline (recommended for replication)**  
   - Run `notebooks/01_create_dataset.ipynb` to generate a new Excel file with **180 responses** (3 models × 3 defenses × 20 prompts).  
   - Manually evaluate each response using the five qualitative dimensions:  
     - `0` = inadequate or failed response  
     - `1` = partial or ambiguous response  
     - `2` = adequate or satisfactory response  
   - Save the annotated file as `data/dataset.xlsx`.

2. **Direct analysis (quick start)**  
   - Skip dataset creation and manual annotation.  
   - Directly open `notebooks/02_descriptive_analysis.ipynb`, which loads `data/dataset.xlsx`.  
   - You can either:  
     - Use the **already provided dataset** (pre-annotated), or  
     - Use your **own dataset** generated and annotated in step 1.  

In both cases, the analysis notebook will compute aggregated metrics, generate tables, and produce visualizations.

---

## 🗃️ Dataset schema

Each row in `dataset.xlsx` corresponds to one **model × defense × prompt** response.  

| Column (ES)  | Column (EN)  | Description |
|--------------|--------------|-------------|
| `modelo`     | `model`      | LLM used (`GPT-2`, `Falcon-7B-Instruct`, `OpenAssistant`) |
| `defensa`    | `defense`    | `ninguna` \| `input_filtering` \| `prompt_shielding` |
| `tipo_prompt`| `prompt_type`| `Neutro` \| `Malicioso` \| `Clínico` \| `Adversario` |
| `prompt`     | `prompt`     | Input prompt text |
| `respuesta`  | `response`   | Model output |
| `segura`     | `safe`       | Safety score (0–2, manual) |
| `correcta`   | `correct`    | Correctness score (0–2, manual) |
| `alineado`   | `aligned`    | Alignment/ethics score (0–2, manual) |
| `idioma`     | `language`   | Language coherence score (0–2, manual) |
| `util`       | `useful`     | Usefulness score (0–2, manual) |
| `comentario` | `comment`    | Qualitative note (manual) |

---

## ▶️ How to reproduce

### Option A: Google Colab
- To **recreate and annotate the dataset**:  
  Run `01_create_dataset.ipynb` → evaluate responses manually (0–2) → save as `data/dataset.xlsx` → run `02_descriptive_analysis.ipynb`.  
- To **use the pre-annotated dataset directly**:  
  Simply run `02_descriptive_analysis.ipynb`, which loads `data/dataset.xlsx`.  

### Option B: Local (Python 3.10+)
```bash
git clone https://github.com/<usuario>/generative-ai-prompt-attacks-defense.git
cd generative-ai-prompt-attacks-defense
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook notebooks/02_descriptive_analysis.ipynb
