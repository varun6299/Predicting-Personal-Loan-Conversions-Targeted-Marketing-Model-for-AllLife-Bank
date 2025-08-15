# 💰 Predicting Personal Loan Conversions — Data-Driven Target Marketing for AllLife Bank
*An end-to-end machine learning project to identify high-probability borrowers among deposit customers, optimize campaign targeting, and boost loan revenue.*

<p align="center">
  <img src="images/personal loan screenshot.png" alt="Income Distribution" width="400"/>
</p>

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.2+-orange.svg)](https://scikit-learn.org/)
[![pandas](https://img.shields.io/badge/pandas-2.0+-green.svg)](https://pandas.pydata.org/)
[![matplotlib](https://img.shields.io/badge/matplotlib-3.7+-yellow.svg)](https://matplotlib.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)

---

## 📜 Project Overview
AllLife Bank, a US-based retail bank, has seen strong growth in its liability customer base — individuals who hold deposit accounts of varying balances. However, the number of asset customers (borrowers) remains small. The bank’s management recognizes a significant revenue opportunity in expanding this segment, particularly in personal loans, which generate interest-based income.

Last year’s personal loan campaign targeted liability customers and achieved a healthy 9% conversion rate. Encouraged by this success, the retail marketing department now seeks to increase this success ratio through better segmentation and targeted marketing.

A past campaign targeted liability customers and achieved a **~9% conversion rate**, sparking interest in **more targeted, data-driven campaigns**.  

This project aims to build a machine learning model that predicts which existing depositors are most likely to accept a personal loan offer, enabling more efficient and profitable marketing campaigns.

1. **Predict** which existing customers are likely to accept a personal loan.
2. **Identify** the customer attributes that influence acceptance.
3. **Segment** the audience for high-impact marketing.

---

## 🎯 Objective
- Build a **predictive model** to classify whether a liability customer will purchase a personal loan.
- **Optimize for recall** — ensure we capture as many likely accepters as possible to maximize loan uptake.
- Maintain good **precision** to avoid wasteful targeting and reduce campaign costs.
- Deliver **business insights** to inform marketing strategy.

---

## 🧾 Dataset Summary
**Features captured:**
- **Demographics:** Age, Experience, Family size, Education level
- **Financials:** Annual Income, Average monthly credit card spend (CCAvg), Mortgage amount
- **Product Holdings:** Securities Account, CD Account, Online Banking usage, Credit Card ownership
- **Target:** `Personal_Loan` — binary indicator of acceptance (1 = accepted, 0 = declined)

---

## 🔍 Key Data Observations
- **Experience:** One invalid negative value flagged (−3 years).
- **Outliers:** High positive skew in Income, CCAvg, and Mortgage; retained due to predictive importance.
- **Irrelevant Features:** ZIP Code dropped (non-predictive).

---

## 📊 Exploratory Data Analysis — Key Insights
### Univariate & Bivariate Findings
- **Income:** Accepters earn ~$142K vs ~$60K for non-accepters — stronger repayment capacity.
- **Credit Card Spend (CCAvg):** Accepters spend ~$3.8K/mo vs ~$1.4K — indicates credit-active behavior.
- **Mortgage:** Accepters’ mortgage ~$288K vs ~$170K — possible refinancing needs.
- **Family Size:** 55% of accepters have 3–4 members — greater financial obligations.
- **Education:** Graduates and Professionals accept more often — tied to income and lifestyle aspirations.
- **CD Accounts:** 30% of accepters vs <10% of non-accepters — cross-sell opportunity.

<p align="center">
  <img src="images/bivariate analysis.png" alt="Income Distribution" width="400"/>
</p>

### Multivariate Patterns
- **High Income + High CCAvg:** Strongest loan acceptance likelihood.
- **High Income + High Mortgage:** Signals refinancing potential.
- **Large Families + High Financial Activity:** Higher acceptance rates.

---

## 🛠 Modeling Approach
- **Algorithm:** Decision Tree Classifier
- **Metric Priority:** Recall (minimize false negatives — avoid missing likely accepters)
- **Variants Tested:**
  1. **Baseline Decision Tree**
  2. **Pre-Pruned Decision Tree** — tuned max depth, min samples split/leaf
  3. **Post-Pruned Decision Tree** — tuned cost complexity (`ccp_alpha`)

---

## 📈 Model Performance

| Model Variant        | CV Recall | Test Recall | Test Precision | Test Accuracy |
|----------------------|-----------|-------------|----------------|---------------|
| Baseline DT          | 0.92      | 0.88        | 0.914          | 0.981         |
| **Pre-pruned DT** ✅ | **0.92**  | **0.89**    | **0.925**      | 0.982         |
| Post-pruned DT       | 0.91      | 0.88        | 0.912          | 0.981         |

**Chosen Model:** **Pre-pruned Decision Tree** — slightly higher precision with equal/better recall compared to baseline, enabling more efficient targeting.

<p align="center">
  <img src="images/confusion martrix - pre-pruned model.png" alt="Income Distribution" width="400"/>
</p>

<p align="center">
  <img src="images/decision tree image.png" alt="Income Distribution" width="400"/>
</p>

---

## 🔍 Feature Importance (Top 5)

<p align="center">
  <img src="images/feature importances.png" alt="Income Distribution" width="400"/>
</p>

1. Income
2. Education
3. Family Size
4. CCAvg
5. Age

---

## 🧠 Business Insights & Recommendations

### **1. Target High-Income Customers**
- **Data Insight:** Customers earning **>$100K/year** have a significantly higher acceptance rate for personal loans (~2.3× higher than average).  
- **Reasoning:** Higher disposable income improves repayment ability and makes customers more open to premium loan offers.  
- **Recommendation:**  
  - Design **exclusive loan tiers** (lower interest rates, flexible tenure) for high-income segments.  
  - Market with lifestyle-driven messaging — e.g., travel, luxury, investment opportunities.

### **2. Engage High Credit Card Spenders (CCAvg)**
- **Data Insight:** Customers spending **>$3K/month** on credit cards are far more likely to accept a personal loan.  
- **Reasoning:** High spenders demonstrate both **credit activity** and **consumption-driven lifestyles**, increasing their likelihood of seeking liquidity.  
- **Recommendation:**  
  - Craft loan offers that complement existing spending patterns (e.g., “festive shopping loan,” “travel upgrade loan”).  
  - Leverage **credit card statement inserts** and **app notifications** for targeted campaigns.

### **3. Focus on Educated Segments**
- **Data Insight:** **Graduate and Professional** degree holders have higher acceptance rates compared to undergraduates.  
- **Reasoning:** Education correlates with higher income and career stability, which reduces credit risk.  
- **Recommendation:**  
  - Position loans as **tools for lifestyle enhancement** (e.g., home improvement, asset purchases).  
  - Offer **career-boost loans** (e.g., executive education, certifications) targeted at professionals.

### **4. Highlight Family Benefits for Larger Households**
- **Data Insight:** **55% of accepters** belong to families with **3–4 members**.  
- **Reasoning:** Larger households have recurring high-value expenses (education, healthcare, housing), creating demand for credit.  
- **Recommendation:**  
  - Offer **family-focused loan products** (e.g., education loans, home renovation loans).  
  - Frame marketing creatives around **family aspirations** (e.g., “Build the future your family deserves”).

### **5. Leverage Cross-Sell Opportunities with CD & Securities Account Holders**
- **Data Insight:** ~**30% of accepters** have **CD accounts** vs <10% among non-accepters.  
- **Reasoning:** These customers already trust the bank and are more receptive to additional products.  
- **Recommendation:**  
  - Bundle **loan + deposit** offers (e.g., “Get a lower loan interest rate when you hold a CD with us”).  
  - Use relationship managers to **personally approach** these high-value customers.

### **6. Combine High-Value Predictors for Segmentation**
- **Data Insight:** Customers with **High Income + High CCAvg + CD Account** membership have the **highest combined acceptance likelihood**.  
- **Recommendation:**  
  - Prioritize this segment for **early campaign waves** to maximize ROI.  
  - Create **lookalike audiences** in marketing platforms based on this profile.

### **7. Optimize Campaign Budget Using Model Scores**
- **Data Insight:** The model’s probability scores allow ranking customers by likelihood of acceptance.  
- **Recommendation:**  
  - Allocate **higher marketing spend** (personalized outreach, premium creatives) to top decile scores.  
  - Use **lighter-touch, automated outreach** (email/SMS) for lower-scoring segments.

---

## 📌 Impact
- **Campaign ROI Boost:** Better targeting means lower spend per conversion.
- **Increased Loan Uptake:** High recall ensures minimal missed opportunities.
- **Strategic Cross-Selling:** Strengthens customer relationship through multi-product holdings.

