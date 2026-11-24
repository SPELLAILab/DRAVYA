<p align="center">
  <img src="assets/dravya-banner.png" alt="DRAVYA: Quantifying Cross-Lingual Cultural Drift Across Dravidian Languages — AAAI-27 Student Abstract" width="100%">
</p>

# DRAVYA: Quantifying Cross-Lingual Cultural Drift Across Dravidian Languages

[![Paper: AAAI 2027](https://img.shields.io/badge/Accepted-AAAI%202027%20Student%20Abstract-0078D4.svg)](https://aaai.org)
[![Benchmark: 20 Dilemmas](https://img.shields.io/badge/Benchmark-20%20Dilemmas%20%7C%201%2C200%20Generations-orange.svg)](data/)

> **Official repository for the AAAI 2027 Student Abstract paper:**  
> *"DRAVYA: Quantifying Cross-Lingual Cultural Drift Across Dravidian Languages"*  
> **Authors:** Shanmukh Datta, Kumar Prateek, Dr. Simranjit Singh  
> **Affiliation:** Dr. B. R. Ambedkar National Institute of Technology Jalandhar  
> **Links:** [Benchmark Data](data/) &nbsp;|&nbsp; [Evaluation Code](code/) &nbsp;|&nbsp; [Results & Tables](docs/BENCHMARK_RESULTS.md)

---

## 📌 About the Paper

When multilingual large language models deployed in non-Western societies are queried on real-life ethical dilemmas, does their counsel shift depending on whether the query is framed in **English, Telugu, Tamil, or Kannada**?

**DRAVYA** is an empirical benchmark investigating cross-lingual cultural value drift and generation stability across the **Dravidian language family** (representing over 250 million native speakers). Evaluating $N = 1,200$ generations across 6 foundation models under both generic and culturally localized conditions across 20 calibrated moral dilemmas, we employ a dual-lens methodology coupling:
1. **Continuous Hofstede Cultural Stance** (1.0 = Western Individualist $\rightarrow$ 5.0 = South Asian Collectivist/Hierarchical), validated through double-blind native human evaluations.
2. **Cross-Lingual Semantic Representation Drift** measured via LaBSE geometric distances ($1 - \cos$).

---

## 🔬 Key Findings

* **Indic Vocabulary Coverage & Stability:** Dedicated Indic foundation models (`sarvam-m`, 24B) achieve **100% clean outputs** (0% repetition loops, 0% truncations), 100% script fidelity, and the lowest semantic representation drift ($\text{LaBSE} = 0.265$), preserving robust cultural alignment across Dravidian prompts.
* **Cultural Entity Priming:** Introducing authentic regional entities (*Venkatesh in Karimnagar*, *Sarpanch*, *Gram Sabha*, *Sankranti*) significantly activates localized collectivist counsel across models ($\Delta_{\text{loc}} \in [+0.24, +0.85]$).
* **The Script Effect:** Presenting dilemmas in native Dravidian scripts yields a significantly higher collectivist stance than English script representations, demonstrating that script acts as an independent cultural activation channel.
* **Double-Blind Human Validation:** Independent evaluations by university-educated native Dravidian speakers confirm strong alignment with automated adjudications ($\kappa_w = 0.590$, with **95.8% agreement within $\pm 1$ point**).

> Full benchmark tables, dimension rankings, and per-language breakdowns are available in [docs/BENCHMARK_RESULTS.md](docs/BENCHMARK_RESULTS.md).

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
  author    = {Datta, Shanmukh and Prateek, Kumar and Singh, Simranjit},
  booktitle = {Proceedings of the AAAI Conference on Artificial Intelligence (Student Abstract and Poster Program)},
  year      = {2027},
  note      = {Accepted for publication}
}
```

---

## 📄 License

This project is licensed under the [MIT License](LICENSE). All benchmark dilemmas, evaluation checkpoints, and code are open for academic research.
