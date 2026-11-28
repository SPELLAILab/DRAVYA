<p align="center">
  <img src="assets/dravya-banner.png" alt="DRAVYA: Quantifying Cross-Lingual Cultural Drift Across Dravidian Languages — AAAI-27 Student Abstract" width="100%">
</p>

# DRAVYA: Quantifying Cross-Lingual Cultural Drift Across Dravidian Languages

[![Paper: AAAI 2027](https://img.shields.io/badge/Accepted-AAAI%202027%20Student%20Abstract-0078D4.svg)](https://aaai.org)
[![Benchmark: 20 Dilemmas](https://img.shields.io/badge/Benchmark-20%20Dilemmas%20%7C%201%2C200%20Generations-orange.svg)](data/)

> **Official repository for the AAAI 2027 Student Abstract paper:**  
> *"DRAVYA: Quantifying Cross-Lingual Cultural Drift Across Dravidian Languages"*  
> **Authors:** Shanmukh Datta, Kumar Prateek, Vijay Kumar, Simranjit Singh  
> **Affiliation:** Dr. B. R. Ambedkar National Institute of Technology Jalandhar  
> **Links:** [Benchmark Data](data/) &nbsp;|&nbsp; [Evaluation Code](code/) &nbsp;|&nbsp; [Results & Tables](docs/BENCHMARK_RESULTS.md)

---

## 📌 About the Paper

When an AI assistant is queried on a real-life moral dilemma—such as taking a high-interest loan to fund a niece's lavish wedding versus preserving savings for a child's university education—Western individualist norms prioritize personal financial autonomy, whereas South Asian collectivist norms emphasize maternal uncle kinship duties (*thaaimaaman / menamama*) and family honor. **Does a model's ethical advice shift simply because the user asks in Telugu, Tamil, or Kannada instead of English?**

**DRAVYA** evaluates this across **20 culturally calibrated dilemmas** ($N = 1,200$ generations at $T=0.0$) over 6 foundation models spanning Western (`Gemma-2-9B`, `Gemma-3-12B`, `Llama-3.1-8B`, `Nemotron-70B`), Eastern (`Qwen-3-8B`), and sovereign Indic (`Sarvam-M`, 24B) provenances.

* **How Global Models React:** Standard BPE global models suffer heavy generation fragility in Dravidian scripts (`31.0%–47.5%` repetition loops in `Nemotron-70B`, `Llama-3.1-8B`, and `Qwen-3-8B`) and shift **directionally toward South Asian collectivism** ($\Delta = +0.12$ to $+0.40$) when queried in Telugu, Tamil, or Kannada rather than English.
* **How Indic Specialization Reacts:** Indic-adapted `Sarvam-M` (24B) eliminates truncation and loops (`100%` clean outputs), yields the lowest cross-lingual semantic drift (`LaBSE = 0.265`), and anchors consistently around a balanced South Asian baseline (`3.05`).

---

## 🧪 Evaluation Framework

1. **Bilingual & Regional Design:** 20 dilemmas balanced across four Hofstede axes (*Individualism/Collectivism, Power Distance, Long-Term Orientation, Indulgence/Restraint*), translated by native linguists into English, Telugu, Tamil, and Kannada under **Generic** (neutral) and **Localized** (regional entities like *panchayats*, *thaaimaaman*) conditions.
2. **Generation Pathology Audit:** All $1,200$ generations are audited for script adherence, truncation, and repetition loops (`23` script failures and `127` truncated outputs excluded $\rightarrow$ `1,050` usable outputs; `1,049` valid scores).
3. **Dual-Lens Measurement & Human Validation:** Clean responses are scored via **GPT-4o** using scenario-specific `1.0–5.0` behavioral anchors and paired with **LaBSE** cross-lingual cosine drift ($1 - \cos$, `570` matched pairs). Stratified double-blind validation by native evaluators ($N = 120$) establishes moderate ordinal agreement ($\kappa_w = 0.590$, **`95.8%` within $\pm 1$ point**; judge-human $\kappa_w = 0.546$, `87.5%` within $\pm 1$).

---

## 🔬 Key Findings

* **Tokenization Fragility Across Provenances:** Larger parameter count alone does not guarantee Dravidian generation stability across differing architectures, corpora, and tokenizers (`Nemotron-70B`: `36.0%` truncation, `31.0%` loops vs. `Sarvam-M`: `0.0%` truncation/loops, `100%` clean outputs).
* **Language-Driven Drift (H1):** In generic dilemmas, Dravidian prompts directionally shift global Western and Eastern models toward collectivist counsel ($\Delta = +0.12$ to $+0.40$), while `Sarvam-M` maintains an anchored baseline ($\Delta = -0.28$, $p = 0.0031^{**}$).
* **Entity Priming & Regional Divergence (H3):** Authentic regional entities trigger a sharp collectivist surge in Telugu across all models ($\Delta_{\text{loc}} \in [+0.24, +0.85]$; `Sarvam-M` $2.35 \rightarrow 3.20$, Wilcoxon $p = 0.002^{**}$), whereas localized Tamil prompts yield mixed or egalitarian shifts reflecting regional social-reform traditions.
* **Hofstede Dimension Vulnerability (H2):** *Collectivism* exhibits the largest net signed shift ($\Delta = +0.262$), followed by *Indulgence* ($\Delta = +0.213$), while *Power Distance* masks high bidirectional volatility ($|\Delta| = 0.54$, net $\Delta = +0.027$).

> Full tables and per-language breakdowns are documented in [docs/BENCHMARK_RESULTS.md](docs/BENCHMARK_RESULTS.md).

---

## 📂 Repository Structure

```text
DRAVYA/
├── README.md                      # Benchmark overview and documentation
├── requirements.txt               # Dependencies
├── LICENSE                        # MIT License
├── assets/
│   ├── dravya-banner.png          # High-resolution benchmark header banner
│   └── nitj_official.png          # Official NIT Jalandhar emblem
│
├── data/                          # Benchmark Scenarios & Scored Outputs
│   ├── all_scenarios.json         # 20 calibrated dilemmas (EN, TE, TA, KN)
│   ├── judge_scores.json          # 1,049 scored evaluations along the Hofstede 1.0-5.0 scale
│   └── embed_distances.json       # 570 cross-lingual LaBSE cosine distances
│
├── results/                       # Consolidated Results & Publication Figures
│   ├── final_table.csv            # Per-model dimension stance and drift
│   ├── model_ranking.csv          # Cross-lingual drift rankings
│   └── figures/                   # Publication-quality vector figures (Figures 1-5, PDF)
│
├── code/                          # Execution & Evaluation Pipeline
│   ├── 01_run_inference.py        # Inference pipeline across foundation models
│   ├── 02_judge_responses.py      # Cultural stance adjudication
│   ├── 03_embed_distance.py       # Cross-lingual semantic embedding distance (LaBSE)
│   └── human_eval/                # Double-blind human validation suite
│
└── docs/                          # Detailed Documentation
    ├── BENCHMARK_RESULTS.md       # Full benchmark data tables (Tables 1-6)
    └── annotator_guidelines.md    # Annotation rubric for native human evaluators
```

---

## ⚡ Quick Start

All 1,200 generations, adjudications, and embedding vectors are pre-computed in this repository. You can reproduce the benchmark metrics and figures directly:

```bash
# 1. Clone repository
git clone https://github.com/SPELLAILab/DRAVYA.git
cd DRAVYA

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run audit reproducing all paper tables
python code/audits/run_full_paper_audit.py

# 4. Compute human agreement statistics (Cohen's Kappa)
python code/human_eval/compute_all_human_agreement.py
```

---

## 📜 Citation

```bibtex
@inproceedings{datta2027dravya,
  title     = {{DRAVYA}: Quantifying Cross-Lingual Cultural Drift Across Dravidian Languages},
  author    = {Datta, Shanmukh and Prateek, Kumar and Kumar, Vijay and Singh, Simranjit},
  booktitle = {Proceedings of the AAAI Conference on Artificial Intelligence (Student Abstract and Poster Program)},
  year      = {2027},
  note      = {Accepted for publication}
}
```

---

## 📄 License

This project is licensed under the [MIT License](LICENSE). All benchmark dilemmas, evaluation checkpoints, and code are open for academic research.
