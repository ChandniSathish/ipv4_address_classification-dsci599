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



### **Cluster Interpretation Table**
| **Cluster** | **Count (IP addresses)** | **Availability (avg)** | **Volatility (avg)** | **RTT Median (avg) (ms)** | **RTT Std Dev (avg)** | **Interpretation** |
|------------|---------------------|-----------------|----------------|----------------|----------------|--------------------|
| 0          | ~7.94M               | 0.000464 (~0.046%)  | 0.9999 (very high) | 0.00072 (~0.7 ms) | 0.0718 | **Mostly unresponsive addresses.** Rarely up, possibly unassigned, firewalled, or ephemeral. Tiny RTT suggests very close router replies or artifacts. |
| 1          | ~2.41M               | 0.996 (99.6% up) | 0.9999 | 45.0 | 0.072 | **Highly stable addresses.** Almost always up, moderate latency, likely servers, infrastructure IPs, or broadband connections. |
| 2          | 94,864               | 0.000847 (~0.085%) | 0.9997 | 170.0 | 0.206 | **Rarely online, high latency.** High RTT and variability suggest satellite links, mobile networks, or remote regions. |

---

### **Overall Observations**
- **All clusters show volatility close to 1.0.**  
  - This might indicate that even a single probe response or missed probe results in a state change.
  - Volatility formula should be reviewed to confirm it captures meaningful toggles rather than noise.
  
- **Median Up = 0 in all clusters.**  
  - This suggests no IP was continuously “up” for multiple consecutive intervals.
  - Possible reasons: data sampling artifacts, or the way median_up is computed.
  - Further refinement in calculating **session lengths** may be needed.

---



