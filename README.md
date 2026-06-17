# Reservoir Nodes: Identifying Drivers and Structural Change in Trade and Mobility Networks

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Data License: CC BY 4.0](https://img.shields.io/badge/Data%20License-CC%20BY%204.0-lightgrey)](https://creativecommons.org/licenses/by/4.0/)
[![Python 3.8+](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![R 4.0+](https://img.shields.io/badge/R-4.0%2B-blue)](https://www.r-project.org/)

Reproducible analytical pipeline for the doctoral dissertation:
**"Reservoir Nodes - Identifying Drivers and Structural Change in Trade and Mobility Networks"**
University of Pannonia, Department of Management, 2026.

---

## Overview

This repository contains the analytical pipeline underpinning the three research questions and theses of the dissertation.

**RQ1** — How do temporal dynamics and causal relationships in trade network indicators vary across products, and what do these patterns reveal about the transmission and impact of shocks, crises, and technological change?

**RQ2** — What do cross-level analyses reveal about the consistency of cultural and institutional determinants of mobility?

**RQ3** — What structural and causal parallels exist between trade and academic mobility networks, and how do they jointly affirm global patterns of interdependence, adaptation, and resilience?

---

## 📊 Key Statistics

| Domain | Metric | Value |
|--------|--------|-------|
| Trade | Database | BACI-CEPII |
| Trade | Countries | 200+ |
| Trade | Products | 5,012 (6-digit HS) |
| Trade | Timespan | 1995–2020 |
| Trade | Network indicators | 10+ per product per year |
| Trade | Derived databases | BACINET3D, BACINODE4D |
| Mobility | Database | Erasmus+ (2008–2013 & 2014–2023) |
| Mobility | Mobile students | 1,162,429 (2008–2013) + 206,448 (2014–2023) |
| Mobility | Institutions | 3,591 (2008–2013) |
| Mobility | NUTS3 regions | 853 active (2008–2013), 1,514 (2014–2023) |
| Mobility | Variables | 70 (2014–2023 dataset) |

---

## 🎯 Citation

If you use this code or data, please cite:

**Dissertation:**
```
Kiss, D. (2026). Reservoir Nodes - Identifying Drivers and Structural Change
in Trade and Mobility Networks. Doctoral Dissertation,
University of Pannonia, Department of Management.
```

**Published papers:**
```
Kosztyán, Z.T., Kiss, D., & Obermayer, N. (2023). Investigating Erasmus mobility
exchange networks with gravity models. Cogent Social Sciences, 9(2), 2253612.

Kosztyán, Z.T., Kiss, D., & Fehérvölgyi, B. (2024). Trade network dynamics in a
globalized environment and on the edge of crises.
Journal of Cleaner Production, 465, 142699.
```

**Erasmus 2014–2023 dataset:**
```
Kiss, D., & Kosztyán, Z.T. (2026). A Multilayer and Spatial Description of the
Erasmus Mobility Network 2014-2023. Figshare.
https://doi.org/10.6084/m9.figshare.31718764
```

**Erasmus 2008–2013 dataset:**
```
Kiss, D. (2026). Student Mobility, Erasmus, 2008-2013. Figshare.
https://doi.org/10.6084/m9.figshare.32716860
```

---

## 🏗️ Repository Structure

```
reservoir-nodes-trade-mobility/
│
├── notebooks/
│   ├── BACI_Full_Pipeline.Rmd
│   └── Erasmus_Gravity_3Cs_FixedEffects.ipynb
│
├── data/                  ← Not hosted here; see Data Sources section
│
├── LICENSE
└── README.md
```

---

## 📦 Data Sources

### Trade — BACI-CEPII
- **Download:** http://www.cepii.fr/cepii/en/bdd_modele/bdd_modele.asp
- **Coverage:** 200+ countries, 1995–2020, 5,012 products (6-digit HS)
- **Format:** CSV, structure: `t | i | j | k | v | q`
  - `t` = year, `i` = exporter (ISO3), `j` = importer (ISO3)
  - `k` = product (6-digit HS), `v` = value (USD), `q` = quantity
- **License:** Free for research use

### Mobility — Erasmus+ (2008–2013)
- **Source:** Kiss, D. (2026), based on Gadár et al. (2020), Scientific Data
- **DOI:** https://doi.org/10.6084/m9.figshare.32716860
- **Coverage:** 1,162,429 students, 194,349 teachers, 3,591 HEIs
- **Enriched with:** ETER, EUROSTAT, Hofstede cultural dimensions at NUTS3

### Mobility — Erasmus+ (2014–2023)
- **Source:** Kiss & Kosztyán (2026)
- **DOI:** https://doi.org/10.6084/m9.figshare.31718764
- **Coverage:** 206,448 records, 70 variables, 1,514 NUTS3 regions
- **Enriched with:** ETER (2022), Eurostat GDP/crime/population, ROR validation

### Cultural Dimensions
- **Source:** Hofstede Insights
- **URL:** https://www.hofstede-insights.com/
- **Variables:** Power distance, individualism, masculinity,
  uncertainty avoidance, long-term orientation, indulgence

### Economic Indicators
- **Source:** Eurostat
- **URL:** https://ec.europa.eu/eurostat
- **Variables:** GDP (NUTS3/NUTS2/Country), crime rates (NUTS2),
  population (NUTS3), gross value added

---

## 📓 Notebooks

### BACI_Full_Pipeline.Rmd
**Purpose:** Build trade networks and compute network/node-level indicators from BACI-CEPII data

- Network-level indicators (value-weighted and volume-weighted): assortativity, centralization, resilience, reciprocity, asymmetry
- Node-level indicators per product group: eigenvector centrality, PageRank, coreness, betweenness, degree in/out
- Granger causality matrix construction across product groups
- World map visualization of trade network structure

### Erasmus_Gravity_3Cs_FixedEffects.ipynb
**Purpose:** Model academic mobility flows with the 3Cs framework and test robustness via fixed effects

- Gravity model specification on the 2014–2023 Erasmus dataset (institutional and NUTS3 levels)
- Random forest regression with cultural (Hofstede), crime, GDP, population, and distance features
- Robustness check: EU membership, shared currency, and shared language as additional dyadic controls
- Poisson pseudo-maximum-likelihood (PPML) estimation with exporter, importer, and year fixed effects, following Anderson & van Wincoop (2003)
- Comparison of which 3Cs effects persist across both random forest and fixed-effects specifications

---

## 🚀 Quick Start

### Requirements

```
Python 3.8+
R 4.0+
4+ GB RAM
```

### Installation

```bash
git clone https://github.com/yrv5wg/reservoir-nodes-trade-mobility.git
cd reservoir-nodes-trade-mobility/notebooks
```

BACI and Erasmus source data are not bundled in this repository — see the Data Sources section above for download links and DOIs. Place downloaded data locally and update the file paths at the top of each notebook before running.

---

## 🔬 Analytical Methods

### Network Indicators

| Indicator | Level | Description |
|-----------|-------|-------------|
| Assortativity | Network | Degree similarity between trading partners |
| Eigenvector centralization | Network | Concentration of centrality |
| Mean coreness | Network | Cohesion of core structure |
| Global clustering | Network | Density of trade clusters |
| Resilience (random) | Network | Robustness to random disruptions |
| Resilience (targeted) | Network | Robustness to targeted attacks |
| Reciprocity | Network | Balance of bilateral trade |
| Bilateral asymmetry | Network | Inequality in trade relationships |
| Betweenness centrality | Node | Brokerage role of countries |
| Eigenvector centrality | Node | Influence of countries |
| Node coreness | Node | Embeddedness in trade core |

### Gravity Model Variables

| Variable | Source | Level |
|----------|--------|-------|
| GDP | Eurostat | NUTS3 |
| Gross value added | Eurostat | NUTS3 |
| Live births | Eurostat | NUTS3 |
| Population density | Eurostat | NUTS3 |
| Crime rate | Eurostat | NUTS2 |
| Institutional collaborations | ETER | Institution |
| International collaborations | ETER | Institution |
| Industry collaborations | ETER | Institution |
| Power distance | Hofstede | NUTS1 |
| Individualism | Hofstede | NUTS1 |
| Masculinity | Hofstede | NUTS1 |
| Uncertainty avoidance | Hofstede | NUTS1 |
| Long-term orientation | Hofstede | NUTS1 |
| Indulgence | Hofstede | NUTS1 |
| Distance | Calculated | Pair |
| EU membership (both/one) | CEPII / own coding | Pair |
| Shared currency (Eurozone) | CEPII / own coding | Pair |
| Shared official language | Own coding | Pair |

---

## ✅ Key Findings

### Thesis 1 — Trade Network Dynamics
The global trade network transitioned from a resilient, diversified structure
into a polarized, dependency-driven system where technological acceleration
and recurrent crises jointly amplify instability.

- Resilience peaked 2013, declined steadily to 2020
- Structural deterioration preceded COVID-19 by 6+ years
- All 5,012 products follow one unified temporal fingerprint
- Shocks propagate through causal architecture, not randomly
- Product group 81 (base metals, tungsten) most sensitive to targeted attack

### Thesis 2 — Mobility Determinants
Cultural determinants consistently influence mobility across institutional,
regional, and national levels — cultural effects are structural, not context-specific.

- Previous gravity models explain <5% of variance
- 3Cs framework (crime, collaboration, culture) raises R² to 33.9% (NUTS3, RF)
- Indulgence and long-term orientation are strongest pull factors
- Masculinity and uncertainty avoidance are strongest push constraints
- Cultural variable importance persists across 2008–2013 and 2014–2023
- EU membership, shared currency, and shared language add no independent explanatory power once gravity fundamentals and country/year fixed effects are accounted for, confirming that cultural and institutional factors — not formal political or monetary integration — drive the result

### Thesis 3 — Structural Parallelism
Global trade and academic mobility networks share fundamentally similar
structural logics: hierarchical organization, preferential attachment,
and dominance of a small number of central actors.

- Both exhibit scale-free properties and rich club structure
- Both show assortativity cycles across time
- Both maintain dominant cores through crises
- Causal propagation follows the same community logic in both domains

---

## 👥 Authors

**Dénes Kiss**
PhD Candidate
University of Pannonia, Faculty of Business and Economics
Veszprém, Hungary
📧 kiss.denes@gtk.uni-pannon.hu

**Zsolt Tibor Kosztyán**
Professor
University of Pannonia, Faculty of Business and Economics
Veszprém, Hungary
📧 kosztyan.zsolt@gtk.uni-pannon.hu

---

## 📜 License

- Code: MIT License
- Data: CC BY 4.0

---

## 🔗 Related Resources

- [BACI-CEPII Database](http://www.cepii.fr)
- [Eurostat](https://ec.europa.eu/eurostat)
- [ETER Project](https://www.eter-project.com/)
- [Erasmus+ 2014–2023 Dataset](https://doi.org/10.6084/m9.figshare.31718764)
- [Erasmus+ 2008–2013 Dataset](https://doi.org/10.6084/m9.figshare.32716860)
- [Gadár et al. (2020)](https://doi.org/10.1038/s41597-020-0382-1)
- [Kosztyán, Kiss & Obermayer (2023)](https://doi.org/10.1080/23311886.2023.2253612)
- [Kosztyán, Kiss & Fehérvölgyi (2024)](https://doi.org/10.1016/j.jclepro.2024.142699)
- [Anderson & van Wincoop (2003)](https://doi.org/10.1257/000282803321455214)

---

## 📅 Version History

**v1.0.0 (2026)** — Initial Release
- BACI network indicator pipeline
- Erasmus gravity model with 3Cs framework
- Fixed-effects robustness check (EU membership, currency, language)

---

*Repository Status:*
📝 Dissertation submitted — University of Pannonia, 2026
🔄 Code actively maintained
