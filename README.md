# 🛍️ Customer Segmentation — RFM Analysis & K-Means Clustering

![Python](https://img.shields.io/badge/Python-3.10-blue) ![scikit-learn](https://img.shields.io/badge/scikit--learn-1.3-orange) ![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

## 📋 Project Summary

Built an unsupervised machine learning pipeline to segment 5,846 customers into four meaningful behavioral groups — uncovering hidden patterns in 776,059 retail transactions. Using RFM analysis (Recency, Frequency, Monetary) and K-Means clustering, the project transforms raw transaction data into actionable customer profiles — enabling personalized marketing strategies, targeted retention campaigns, and smarter resource allocation.

---

## 💼 Business Context

Treating all customers the same wastes marketing resources and misses retention opportunities. This project answers the question every marketing team needs answered:

> *"Who are our customers — and how should we treat each group differently?"*

Without segmentation a business cannot distinguish between its most valuable Champions and its At-Risk customers on the verge of leaving — resulting in generic campaigns that resonate with no one.

---

## 📊 Dataset Overview

| Field | Detail |
|---|---|
| **Source** | UCI Online Retail Dataset — Kaggle |
| **Raw Size** | 1,067,371 transactions × 8 features |
| **Clean Size** | 776,059 transactions — 72.7% retained |
| **Unique Customers** | 5,846 |
| **Period** | 2010 — 2011 |
| **Region** | UK-based online retailer |

---

## 🔬 Methodology

### 1. Data Cleaning
Systematic removal of invalid records before any analysis:

| Step | Rows Removed | Reason |
|---|---|---|
| Missing CustomerID | 243,007 | RFM requires customer identity |
| Negative Quantities | 18,744 | Cancelled orders |
| Zero/Negative Prices | 71 | Invalid transactions |
| Non-standard StockCodes | 2,917 | Postage, fees, discounts |
| Duplicates | 26,055 | Data quality issues |
| Unspecified Country | 518 | Ambiguous attribution |
| **Final Dataset** | **776,059** | **72.7% retained** |

### 2. RFM Feature Engineering
Three behavioral dimensions engineered per customer:

| Feature | Formula | Meaning |
|---|---|---|
| **Recency** | Days since last purchase (ref: 2012-01-01) | How recently did they buy? |
| **Frequency** | Count of unique invoices | How often do they return? |
| **Monetary** | Sum of Quantity × Price | How much do they spend? |

### 3. Preprocessing
- **Log Transformation** — compressed right-skewed RFM distributions to prevent scale domination in distance calculations
- **StandardScaler** — normalized all features to mean≈0, std≈1 — confirmed equal contribution to K-Means clustering

### 4. Optimal K Selection
- **Elbow Method** — inertia plotted for K=1 to K=10 — elbow identified at K=4-5
- **Silhouette Score** — highest at K=2 (0.4348) but insufficient business granularity
- **Final Decision** — K=4 selected (Silhouette = 0.3847) — balancing statistical validity with business interpretability

### 5. PCA Visualization
- Reduced 3D RFM space to 2D for visual cluster inspection
- PC1 = 76%, PC2 = 19% — **95% of variance retained**
- Four clusters visually distinguishable with natural boundary overlap

---

## 🎯 Customer Segments

| Segment | Recency | Frequency | Monetary | Size |
|---|---|---|---|---|
| **Champions** | Lowest — most recent | Highest | Highest | 1,358 |
| **Loyal Customers** | Moderate | Moderate | Good | 1,215 |
| **Promising Customers** | Recent | Low | Moderate | 1,569 |
| **At-Risk Customers** | Highest — least recent | Lowest | Lowest | 1,704 |

---

## 🔍 Key Findings

- **Champions** are behaviorally unique — highest on all three RFM dimensions simultaneously — appearing most distinctly separated in PCA visualization
- **Frequency and Monetary are positively correlated** — strategies that increase visit frequency naturally drive revenue growth without separate spend incentives
- **At-Risk customers** represent the largest segment (1,704) — urgent intervention required before permanent loss
- **Log transformation was essential** — raw RFM distributions were heavily right-skewed and would have produced scale-driven clusters rather than behavioral ones
- **95% of RFM variance** preserved in 2D PCA visualization — confirming reliable cluster representation

---

## 💡 Business Recommendations

**🏆 Champions — Retain & Reward**
Launch an exclusive VIP program offering early access to new products, premium discounts, and invitation-only events. This segment represents the highest business value — increasing switching costs through exclusivity protects the most profitable customer relationships.

**💛 Loyal Customers — Re-engage & Personalize**
Deploy a personalized recommendation engine based on individual purchase history — delivering targeted communications featuring products aligned with demonstrated preferences. Goal: rebuild purchase frequency before these customers drift toward At-Risk.

**🌱 Promising Customers — Convert & Incentivize**
Introduce a loyalty points system where customers earn redeemable points for every purchase — exchangeable for free products or discounts. Incentivizes repeat visits and accelerates progression toward Loyal Customer status.

**⚠️ At-Risk Customers — Win Back Urgently**
Deploy a win-back campaign for customers inactive for over 100 days — combining time-sensitive discounts with a short satisfaction survey to identify pain points. Early intervention is critical — customers inactive beyond this window are significantly harder to recover.

---

## 🛠️ Tech Stack

```
Python          3.10
pandas          2.0
numpy           1.24
scikit-learn    1.3
matplotlib      3.7
seaborn         0.12

---

## ▶️ How To Run

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/customer-segmentation.git

# 2. Navigate to project directory
cd customer-segmentation

# 3. Install dependencies
pip install -r requirements.txt

# 4. Launch Jupyter Notebook
jupyter notebook notebooks/customer_segmentation.ipynb

# 5. Run all cells
```

> **Note:** Dataset available on [Kaggle](https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci). Download and place in `data/` folder before running.

---

## 📈 Future Improvements

- [ ] Add radar chart visualization to profile each segment's RFM personality
- [ ] Incorporate product category data for richer customer profiling
- [ ] Build automated pipeline to re-segment customers monthly
- [ ] Deploy segmentation results into a live marketing dashboard

---

## 👤 Author

**Mustafa Ahmed**
🐙 [GitHub](https://github.com/yourusername)

---
