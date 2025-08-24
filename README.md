# generative-ai-prompt-attacks-defense

Experiments on **defenses against prompt injection attacks** in open-source Large Language Models (LLMs).  
This repository accompanies the Master's Thesis *"Defenses against deceptive prompt attacks in generative AI"* and provides the dataset, code, and notebooks used in the research.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/mujikane/generative-ai-prompt-attacks-defense)

---

## 📂 Repository structure

- `data/`
  - `datos_modelo_tfm.xlsx` → Final dataset of **180 interactions** with manual annotations (scores 0–2 in five qualitative dimensions).
- `notebooks/`
  - `01_create_dataset.ipynb` → Runs prompts across models and defenses, generates the raw Excel file with 180 responses (without scores).
  - `02_descriptive_analysis.ipynb` → Loads the manually annotated Excel (`datos_modelo_tfm.xlsx`) and performs descriptive and quantitative analysis.
- `results/`
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
   - Save the annotated file as `data/datos_modelo_tfm.xlsx`.

2. **Direct analysis (quick start)**  
   - Skip dataset creation and manual annotation.  
   - Directly open `notebooks/02_descriptive_analysis.ipynb`, which loads `data/datos_modelo_tfm.xlsx`.  
   - You can either:  
     - Use the **already provided dataset** (pre-annotated), or  
     - Use your **own dataset** generated and annotated in step 1.  

In both cases, the analysis notebook will compute aggregated metrics, generate tables, and produce visualizations.

---

## 🗃️ Dataset schema

Each row in `datos_modelo_tfm.xlsx` corresponds to one **model × defense × prompt** response.  

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
  Run `01_create_dataset.ipynb` → evaluate responses manually (0–2) → save as `data/datos_modelo_tfm.xlsx` → run `02_descriptive_analysis.ipynb`.  
- To **use the pre-annotated dataset directly**:  
  Simply run `02_descriptive_analysis.ipynb`, which loads `data/datos_modelo_tfm.xlsx`.  

### Option B: Local (Python 3.10+)
```bash
git clone https://github.com/mujikane/generative-ai-prompt-attacks-defense.git
cd generative-ai-prompt-attacks-defense
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook notebooks/02_descriptive_analysis.ipynb
```

---

## 🌐 Language notice

The Jupyter/Colab notebooks (`notebooks/01_create_dataset.ipynb`, `notebooks/02_descriptive_analysis.ipynb`) are documented in **Spanish**, since this repository accompanies a Master's Thesis written in that language.  

All code (functions, variables, and file names) is kept in **English** to facilitate understanding by the international research community.

---

## 📊 Key metrics

- **ASR (Attack Success Rate)** → % of malicious prompts that induced unsafe output.  
- **Correct Refusal Rate** → % of malicious prompts safely refused.  
- **Mean scores per dimension** → seguridad, corrección, alineamiento, idioma, utilidad.  

---

## ⚖️ Ethics & safety

- No personal data is included.  
- Clinical prompts are synthetic and for research only.  
- The code and dataset must **not** be used to deploy unsafe models.  

---

## 📚 Citation

If you use this repository, please cite:

```bibtex
@misc{tfm_2025_prompt_defense,
  title        = {Defenses against prompt attacks in generative AI},
  author       = {Ane Múgica Urbina},
  year         = {2025},
  url          = {https://github.com/mujikane/generative-ai-prompt-attacks-defense}
}
```

---

## 📝 License

MIT License – see [LICENSE](LICENSE).
