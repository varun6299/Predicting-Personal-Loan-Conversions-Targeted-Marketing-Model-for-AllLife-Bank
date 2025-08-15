# Predicting Personal Loan Conversions - Targeted Marketing Model for AllLife Bank

# 📊 Personal Loan Campaign — Customer Conversion Modeling

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.2+-orange.svg)](https://scikit-learn.org/)
[![pandas](https://img.shields.io/badge/pandas-2.0+-green.svg)](https://pandas.pydata.org/)
[![matplotlib](https://img.shields.io/badge/matplotlib-3.7+-yellow.svg)](https://matplotlib.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)

---

## 📌 Problem
AllLife Bank wants to **convert more depositors into personal loan customers** to grow loan revenue.  
We build a **recall-optimized Decision Tree** model to identify likely accepters and surface actionable drivers for targeted marketing.

---

## 🧾 Data
- **Demographics:** Age, Experience, Family size, Education level
- **Financials:** Income, CCAvg (monthly credit card spend), Mortgage
- **Products:** Securities Account, CD Account, Online Banking
- **Target:** `Personal_Loan` (1 = accepted, 0 = declined)

---

## 🔍 EDA — Key Visual Insights

| Feature                | Observation |
|------------------------|-------------|
| **Income**             | Accepters earn ~2.3× more than non-accepters |
| **Credit Card Spend**  | Accepters spend ~2.7× more monthly |
| **Education**          | Higher acceptance among graduates & professionals |
| **Family Size**        | Larger families (3–4 members) show higher acceptance |
| **CD Accounts**        | Strong cross-sell potential — 3× higher incidence among accepters |

<p align="center">
  <img src="images/income_distribution.png" alt="Income Distribution" width="400"/>
  <img src="images/ccavg_distribution.png" alt="CCAvg Distribution" width="400"/>
</p>

<p align="center">
  <img src="images/education_vs_acceptance.png" alt="Education vs Acceptance" width="400"/>
  <img src="images/family_vs_acceptance.png" alt="Family Size vs Acceptance" width="400"/>
</p>

---

## 🛠 Modeling Approach
- **Algorithm:** Decision Tree Classifier
- **Primary Metric:** Recall (reduce missed likely accepters)
- **Variants Tested:**  
  1. Baseline Decision Tree  
  2. Pre-pruned (max depth, min samples split/leaf)  
  3. Post-pruned (cost complexity `ccp_alpha`)

---

## 📈 Results Comparison

| Model Variant        | CV Recall | Test Recall | Test Precision | Test Accuracy |
|----------------------|-----------|-------------|----------------|---------------|
| Baseline DT          | 0.92      | 0.88        | 0.914          | 0.981         |
| **Pre-pruned DT** ✅ | **0.92**  | **0.89**    | **0.925**      | 0.982         |
| Post-pruned DT       | 0.91      | 0.88        | 0.912          | 0.981         |

> **Chosen Model:** Pre-pruned DT — better precision with equal/better recall.

---

## 🧠 Business Takeaways
1. **Target high-income** depositors with premium benefit messaging.
2. **Engage high CCAvg spenders** with personalized offers matching spending categories.
3. **Focus on educated segments** — position loans as enablers for professional/lifestyle growth.
4. **Highlight family benefits** for larger households.
5. **Cross-sell to CD/Securities account holders** to leverage trust and loyalty.

---

## 🛠️ Tech Stack
- Python 3.10+
- pandas, numpy, matplotlib, seaborn
- scikit-learn (DecisionTreeClassifier, GridSearchCV)
- Jupyter Notebook

---

## 🚀 How to Run

```bash
# 1) Clone repository
git clone https://github.com/<your-username>/personal-loan-campaign.git
cd personal-loan-campaign

# 2) Create virtual environment & install dependencies
python -m venv .venv
source .venv/bin/activate    # Windows: .venv\Scripts\activate
pip install -r requirements.txt

# 3) Run notebook
jupyter notebook notebooks/loan_campaign_analysis.ipynb
