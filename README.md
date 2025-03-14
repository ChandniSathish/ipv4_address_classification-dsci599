# **Machine-Learning Analysis of Derived Features to Understand IP Address Usage**  
*Interim Report for Research Project B*

---

## **Table of Contents**
1. [Overview](#overview)  
2. [Repository Contents](#repository-contents)  
3. [Getting Started](#getting-started)  
4. [Usage & Scripts](#usage--scripts)  
5. [Data Description](#data-description)  
6. [Results & Outputs](#results--outputs)  
7. [Future Work](#future-work)  
8. [References](#references)

---

<a name="overview"></a>
## **1. Overview**
This repository explores how **machine learning** can characterize **IP address usage** patterns. We derive features from active-probing data (e.g., availability, volatility, and RTT statistics) and feed these into both **unsupervised** (K-Means) and **supervised** (RandomForest) models to classify IP addresses as:
- **Always-on** (near 100% availability)
- **Rarely responsive** (low availability)
- **High-latency** or **ephemeral** (potentially behind NAT or DHCP)

**Key Objectives**  
- Understand address blocks that are consistently online vs. highly variable.  
- Integrate reverse DNS analysis for label generation.  
- Explore potential ISP and security applications.

---

<a name="repository-contents"></a>
## **2. Repository Contents**
```plaintext
.
├── data/
│   ├── raw/               # Unprocessed raw CSV files (if provided)
│   ├── processed/         # Cleaned or merged datasets after preprocessing
│   └── README.md          # Details on data sources and schema
├── notebooks/
│   └── dsci599.ipynb      # Jupyter notebook with data cleaning & ML analysis
├── scripts/
│   ├── cluster_analysis.py # Python script for K-Means and DBSCAN clustering
│   ├── dns_lookup.py       # Bulk reverse DNS lookups & pattern extraction
│   └── train_model.py      # Training & evaluating supervised models
├── results/
│   ├── figures/           # Generated plots (clusters, metrics, etc.)
│   ├── tables/            # Summary statistics & cluster metrics
│   └── logs/              # Logs from long-running scripts
├── README.md              # This file
└── requirements.txt       # Python dependencies
