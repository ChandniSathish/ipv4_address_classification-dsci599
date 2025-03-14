# **Detecting Carrier-Grade NAT (CGNAT) and DHCP-Based IP Allocation Using ML**

## **Project Overview**
This project aims to **detect and classify IP addresses** (and address blocks) that are:
- **Carrier-Grade NAT (CGNAT)** shared IPs
- **DHCP-based (dynamic) IP allocations**
- **Static public IPs**

We use **machine-learning (ML)** to analyze derived features (e.g., availability, volatility, median RTT) from large-scale active-probing data. Our goal is to move beyond traditional threshold-based methods (e.g., Cai et al.) and apply **clustering** and **classification** techniques to discover nuanced patterns.

## **Repository Contents**
- **`dsci599.ipynb`**  
  - A Jupyter notebook that includes:
    - **Data Cleaning**: Reads the large CSV with derived features, drops placeholders, handles NaNs.  
    - **Feature Engineering**: Refines `volatility` or `median_up` calculations.  
    - **Clustering**: Uses **K-Means or DBSCAN** to group IP addresses.  
    - **Classification**: If labels (e.g., from reverse DNS) are available, trains **RandomForest/XGBoost**.
    - **Analysis & Plots**: Summarizes clusters, sample visualizations (e.g., availability distributions).

- **`requirements.txt`** *(optional)*  
  - Lists Python dependencies (`pandas`, `numpy`, `scikit-learn`, `matplotlib`, `requests`, etc.).

- **Data Files**  
  - **Large CSV (~4GB)** with columns:
    ```
    probe_addr, availability, volatility, median_up, median_rtt, std_rtt
    ```
git clone https://github.com/ChandniSathish/ipv4_address_classification-dsci599.git

## **6. Results & Outputs**

### **Clustering Results**
- K-Means outputs cluster labels categorizing IPs into groups such as:
  - **Always-up**
  - **Rarely-up**
  - **High-latency**
  - **Ephemeral IPs**
  
### **Supervised Classification**
- **RandomForest/XGBoost** performance metrics:
  - **Confusion Matrix**
  - **Feature Importances**
  - **Accuracy, Precision, Recall, F1-Score**

### **Graphs & Tables**
- Visual results are stored in:
  - **Figures Directory** → `results/figures/`
  - **Tables Directory** → `results/tables/`

### **Example: Cluster Interpretation Table**
| **Cluster** | **Availability (avg)** | **Volatility (avg)** | **RTT Median (avg)** | **Interpretation** |
|------------|---------------------|-----------------|----------------|--------------------|
| 0          | 0.001               | 1.0             | 0.0007         | Mostly unresponsive, ephemeral toggles |
| 1          | 0.996               | 1.0             | 0.045          | Highly stable, moderate latency |
| 2          | 0.0008              | 0.5             | 0.170          | Rarely online, but very high latency |
| 3          | ...                 | ...             | ...            | ... |


