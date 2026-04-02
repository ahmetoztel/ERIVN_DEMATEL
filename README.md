# ERIVN-DEMATEL

**Empirical Rule Interval-Valued Neutrosophic DEMATEL**

This repository contains the Python implementation of the ERIVN-DEMATEL methodology and its validation simulation, accompanying the paper:

> *[Paper Title]* — [Authors] — [Journal], [Year]  
> DOI: [DOI link]

---

## Overview

ERIVN-DEMATEL is a novel multi-criteria decision-making (MCDM) methodology that integrates single-valued neutrosophic expert elicitation with interval-valued neutrosophic computation through a statistically grounded transformation. Rather than requiring experts to directly provide interval-valued judgments, ERIVN-DEMATEL:

1. Collects individual expert opinions as **Single-Valued Neutrosophic Numbers (SVNNs)** using a standardized five-point linguistic scale
2. Derives interval bounds via the **empirical rule** (mean ± standard deviation), capturing both consensus and dispersion of expert assessments
3. Applies **deneutrosophication** to produce crisp values for the DEMATEL procedure
4. Classifies factors into **cause** and **effect** groups via prominence (*D*+*R*) and relation (*D*−*R*) scores

---

## Repository Structure

```
ERIVN_DEMATEL/
│
├── ERIVN_DEMATEL.py            # Main implementation: data input, IVNN construction,
│                               # DEMATEL calculations, Excel output, causal diagram
│
├── validation_simulation.py    # Monte Carlo validation (10,000 runs):
│                               # - Comparative analysis vs Classical/Fuzzy/NS/IVN-DEMATEL
│                               # - Sensitivity analysis (δ = 5%, 10%, 20%)
│                               # - Real data application
│
└── README.md
```

---

## Requirements

```
Python >= 3.9
numpy
pandas
scipy
matplotlib
openpyxl
```

Install dependencies:

```bash
pip install numpy pandas scipy matplotlib openpyxl
```

---

## Usage

### ERIVN-DEMATEL Application (`ERIVN_DEMATEL.py`)

Run the script and select your Excel input file via the file dialog. The input file should contain expert opinion matrices stacked vertically without gaps — each expert's *n* × *n* matrix placed one below the other, using the 0–4 linguistic scale.

```bash
python ERIVN_DEMATEL.py
```

**Outputs:**
- `ERIVN_DEMATEL_Results_English.xlsx` — DEMATEL results, Z/X/T matrices, IVNN matrix
- `DEMATEL_Causal_Diagram_English.pdf` — Cause-effect diagram

### Validation Simulation (`validation_simulation.py`)

Runs the full 10,000-run Monte Carlo simulation comparing ERIVN-DEMATEL against four established variants, and applies all methods to the real dataset.

```bash
python validation_simulation.py
```

**Note:** The real data path is set to `Textile_Input.xlsx` in the same directory. Update the path in the script if needed.

**Outputs:**
- `Validation_Results.xlsx` — Summary statistics and raw simulation data across all sheets

---

## Linguistic Scale

Expert judgments are collected using the following five-point scale, mapped to Single-Valued Neutrosophic Numbers (SVNNs) adapted from Biswas et al. (2016):

| Score | Linguistic Term | *T* | *I* | *F* |
|-------|----------------|-----|-----|-----|
| 0 | No Influence (NI) | 0.10 | 0.80 | 0.90 |
| 1 | Very Low Influence (VL) | 0.35 | 0.60 | 0.70 |
| 2 | Low Influence (L) | 0.50 | 0.40 | 0.45 |
| 3 | High Influence (H) | 0.80 | 0.20 | 0.15 |
| 4 | Very High Influence (VH) | 0.90 | 0.10 | 0.10 |

---

## IVNN Construction via Empirical Rule

For each pairwise relationship (*i*, *j*), the interval bounds are derived from *q* expert assessments as:

$$T_x^L = \max(0,\ \bar{T}_x - \sigma_{T_x}), \quad T_x^U = \min(1,\ \bar{T}_x + \sigma_{T_x})$$

and analogously for the indeterminacy (*I*) and falsity (*F*) components. The resulting IVNN is deneutrosophicated using the operator of Karasan et al. (2022).

---

## Validation Design

The simulation compares ERIVN-DEMATEL against:

| Method | Uncertainty Representation |
|--------|---------------------------|
| Classical DEMATEL | Crisp mean scores |
| Fuzzy DEMATEL | Triangular fuzzy numbers (Wu & Lee, 2007) |
| NS-DEMATEL | Single-valued neutrosophic numbers (Biswas et al., 2016) |
| IVN-DEMATEL | Interval-valued neutrosophic numbers (Al-Quran et al., 2020) |

**Similarity metrics** (Section 3.2 of the paper):
- *ρ*<sub>D+R</sub> — Spearman rank correlation of prominence scores
- *ρ*<sub>D−R</sub> — Spearman rank correlation of relation scores
- *d*<sub>norm</sub> — Normalized Euclidean distance

**Sensitivity analysis:** δ ∈ {0.05, 0.10, 0.20} perturbation of expert assessments.

---

## Citation

If you use this code in your research, please cite:

```bibtex
@article{[citekey],
  author  = {[Authors]},
  title   = {[Paper Title]},
  journal = {[Journal]},
  year    = {[Year]},
  doi     = {[DOI]}
}
```

---

## References

- Biswas, P., Pramanik, S., & Giri, B. C. (2016). TOPSIS method for multi-attribute group decision-making under single-valued neutrosophic environment. *Neural Computing and Applications*, 27(3), 727–737.
- Wu, W.-W., & Lee, Y.-T. (2007). Developing global managers' competencies using the fuzzy DEMATEL method. *Expert Systems with Applications*, 32(2), 499–507.
- Al-Quran, A., Hashim, H., & Abdullah, L. (2020). A hybrid approach of interval neutrosophic vague sets and DEMATEL with new linguistic variable. *Symmetry*, 12(2), 275.
- Karasan, A., Ilbahar, E., Cebi, S., & Kahraman, C. (2022). Customer-oriented product design using an integrated neutrosophic AHP & DEMATEL & QFD methodology. *Applied Soft Computing*, 118, 108445.
- Gabus, A., & Fontela, E. (1972). *World problems, an invitation to further thought within the framework of DEMATEL*. Battelle Geneva Research Center.

---

## License

This project is licensed under the MIT License.
