# DRAVYA: Comprehensive Benchmark Tables & Statistical Audits

This document contains the complete, unabridged benchmark evaluations, generation pathology audits, and statistical hypothesis tests for the paper:
**"DRAVYA: Quantifying Cross-Lingual Cultural Drift Across Dravidian Languages"**.

All reported figures reflect the empirical data across $N = 1,200$ generations across 6 foundation models, 4 languages, and 20 calibrated moral dilemmas.

---

## Table 1: Generation Quality & Pathology Audit (1,200 Outputs)

| Model Identifier | Raw $N$ | Script Adherence | 1st-Pass Truncation | Final Truncation | Degeneration Loop Rate | Clean Scored $N$ | Complete Output % |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **`sarvam_m`** | 200 | **200 / 200 (100.0%)** | **0.0% (0 / 200)** | **0.0% (0 / 200)** | **0.0% (0 / 200)** | **200 / 200** | **100.0%** |
| **`gemma3_12b`** | 200 | 198 / 200 (99.0%) | **0.0% (0 / 200)** | **0.0% (0 / 200)** | **0.0% (0 / 200)** | 198 / 200 | 99.0% |
| **`gemma2_9b`** | 200 | 179 / 200 (89.5%) | 0.5% (1 / 200) | 0.5% (1 / 200) | 1.0% (2 / 200) | 178 / 200 | 89.0% |
| **`llama31_8b`** | 200 | 200 / 200 (100.0%) | 25.5% (51 / 200) | 13.0% (26 / 200) | 39.0% (78 / 200) | 174 / 200 | 87.0% |
| **`qwen3_8b`** | 200 | 200 / 200 (100.0%) | 34.0% (68 / 200) | 14.0% (28 / 200) | 47.5% (95 / 200) | 171 / 200 | 85.5% |
| **`llama-3.1-nemotron-70b`** | 200 | 200 / 200 (100.0%) | **36.0% (72 / 200)** | **36.0% (72 / 200)** | **31.0% (62 / 200)** | **128 / 200** | **64.0%** |
| **Total / Pooled** | **1,200** | **1,177 / 1,200 (98.1%)** | **15.9% (191 / 1,200)** | **10.6% (127 / 1,200)** | **19.8% (237 / 1,200)** | **1,049 / 1,200** | **87.4%** |

*Note: Complete % reflects non-truncated, script-adherent outputs scored along the 1.0–5.0 Hofstede continuum.*

---

## Table 2: Cross-Lingual Cultural Stance Drift (Generic Condition)

$$\Delta = \text{Stance}_{\text{Dravidian}} - \text{Stance}_{\text{English}}$$
*(Hofstede continuum: 1.0 = Western Individualist $\rightarrow$ 5.0 = South Asian Collectivist/Hierarchical)*

| Model Architecture | EN Baseline | Telugu (`TE`) | Tamil (`TA`) | Kannada (`KN`) | $\Delta$(TE) | $\Delta$(TA) | $\Delta$(KN) | Mean Drift ($\Delta$) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **`gemma2_9b`** | 2.55 | 2.69 | 2.65 | 3.50 | $+0.14$ | $+0.10$ | $+0.95$ | **$+0.396$** |
| **`llama31_8b`** | 2.60 | 3.13 | 3.00 | 2.79 | $+0.53$ | $+0.40$ | $+0.19$ | **$+0.374$** |
| **`llama-3.1-nemotron-70b`** | 2.55 | 2.33 | 3.56 | 2.75 | $-0.22$ | $+1.01$ | $+0.20$ | **$+0.330$** |
| **`qwen3_8b`** | 2.35 | 2.33 | 2.86 | 2.27 | $-0.02$ | $+0.51$ | $-0.08$ | **$+0.136$** |
| **`gemma3_12b`** | 2.65 | 2.50 | 2.75 | 3.05 | $-0.15$ | $+0.10$ | $+0.40$ | **$+0.117$** |
| **`sarvam_m`** | 3.05 | 2.35 | 3.00 | 2.95 | $-0.70$ | $-0.05$ | $-0.10$ | **$-0.283$** |

---

## Table 3: Cultural Localization Shift (Hypothesis 3)

$$\Delta_{\text{loc}} = \text{Stance}_{\text{Localized}} - \text{Stance}_{\text{Generic}}$$

| Model Identifier | $\Delta_{\text{loc}}$(EN) | Telugu ($\Delta_{\text{loc}}$) | Tamil ($\Delta_{\text{loc}}$) | Kannada ($\Delta_{\text{loc}}$) | Empirical Significance |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **`sarvam_m`** | $-0.13$ | **$+0.85$** ($2.35 \rightarrow 3.20$) | $-0.20$ | $+0.00$ | **Significant shift (Wilcoxon $p = 0.0020^{**}$)** |
| **`llama-3.1-nemotron-70b`** | $+0.35$ | **$+0.78$** ($2.33 \rightarrow 3.11$) | $-0.92$ | $-0.15$ | High Telugu collectivist surge |
| **`llama31_8b`** | $+0.25$ | **$+0.41$** ($3.13 \rightarrow 3.54$) | $+0.33$ | $+0.10$ | Positive shift across all languages |
| **`gemma3_12b`** | $-0.03$ | **$+0.35$** ($2.50 \rightarrow 2.85$) | $-0.10$ | $-0.44$ | Telugu collectivist shift |
| **`gemma2_9b`** | $-0.02$ | **$+0.25$** ($2.69 \rightarrow 2.94$) | $-0.10$ | $-0.63$ | Moderate Telugu shift |
| **`qwen3_8b`** | $+0.42$ | **$+0.24$** ($2.33 \rightarrow 2.57$) | $-0.72$ | $+0.07$ | Moderate Telugu shift |

---

## Table 4: Cross-Lingual Semantic Stability (LaBSE Embedding Distance: $1 - \cos$)

| Model Architecture | $\text{EN}\rightarrow\text{TE}$ | $\text{EN}\rightarrow\text{TA}$ | $\text{EN}\rightarrow\text{KN}$ | Mean Semantic Drift ($\downarrow$) | Cosine Similarity ($\uparrow$) | Valid Pairs ($N$) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **`sarvam_m`** | **0.2612** | **0.2545** | **0.2803** | **0.2653** | **0.7347** | 120 / 120 (100%) |
| **`gemma2_9b`** | 0.2643 | 0.2672 | 0.2895 | **0.2719** | **0.7281** | 98 / 120 (81.7%) |
| **`nemotron-70b`** | 0.3112 | 0.3230 | 0.3369 | **0.3231** | **0.6769** | 48 / 120 (40.0%) |
| **`gemma3_12b`** | 0.3233 | 0.3237 | 0.3269 | **0.3246** | **0.6754** | 118 / 120 (98.3%) |
| **`qwen3_8b`** | 0.3356 | 0.3294 | 0.3659 | **0.3445** | **0.6555** | 92 / 120 (76.7%) |
| **`llama31_8b`** | 0.3524 | 0.3692 | 0.3816 | **0.3691** | **0.6309** | 94 / 120 (78.3%) |

---

## Table 5: Double-Blind Native Human Validation ($N=120$)

| Model Identifier | Sample $n$ | Inter-Ann $\kappa_u$ | Inter-Ann $\kappa_w$ | Inter-Ann $\pm 1$ (%) | Exact Match (%) | Judge-Human $\kappa_w$ | Judge-Human $\pm 1$ (%) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **`qwen3_8b`** | 20 | 0.433 | **0.654** | **100.0%** | 60.0% | 0.568 | 85.0% |
| **`sarvam_m`** | 20 | 0.542 | **0.649** | **100.0%** | 70.0% | 0.380 | 90.0% |
| **`gemma2_9b`** | 20 | **0.558** | **0.638** | **100.0%** | **75.0%** | 0.515 | 92.5% |
| **`llama31_8b`** | 20 | 0.373 | **0.609** | **100.0%** | 50.0% | 0.556 | 87.5% |
| **`nemotron-70b`** | 20 | 0.375 | 0.539 | 80.0% | 50.0% | **0.764** | 90.0% |
| **`gemma3_12b`** | 20 | 0.106 | 0.336 | 95.0% | 20.0% | 0.229 | 80.0% |
| **Pooled Benchmark** | **120** | **0.392** | **0.590** | **95.8%** | **54.2%** | **0.546** | **87.5%** |

---

## Table 6: Hofstede Dimension Vulnerability Hierarchy

| Hofstede Cultural Dimension | Scored $N$ | EN Baseline | Dravidian Mean | Net Drift ($\Delta$) | Mean Absolute Shift ($|\Delta|$) | Observed Behavior |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| **Collectivism vs. Individualism** | 100 | 2.57 | 2.83 | **+0.262** | **0.62** | **Highest net collectivist shift** |
| **Indulgence vs. Restraint** | 105 | 3.27 | 3.48 | **+0.213** | 0.44 | High shift toward modesty & duty |
| **Long-Term Orientation** | 94 | 2.20 | 2.27 | +0.066 | 0.38 | Highly invariant across languages |
| **Power Distance** | 105 | 2.47 | 2.49 | +0.027 | **0.54** | High volatility across languages |
