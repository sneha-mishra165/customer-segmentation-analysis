# 🛒 E-Commerce Customer Segmentation Engine

An end-to-end data engineering and unsupervised machine learning pipeline that consumes messy behavioral retail transactions from a raw local Excel file, engineers dynamic **RFM (Recency, Frequency, Monetary)** customer profiles, and applies **K-Means Clustering** to segment an active user base into strategic corporate marketing groups.

---

## 📊 Executive Dashboard Summary
Our final analytical findings are exported into an enterprise-ready Power BI dashboard, optimized with modern visual UX rules (rounded card containers, intentional whitespace, high-contrast typography) to offer instant corporate tracking:

*👉 [Power BI dashboard here!]*

---

## 🧬 Data Pipeline Architecture & Insights

### 🧭 Module 01: Rigorous Data Cleansing
The raw source Excel dataset contained **541,909 raw transaction records** with significant operational noise. The following data engineering transformations were executed to protect model training:
*   **Anonymous Tracking Drop:** Purged **135,080 rows** completely missing a valid `CustomerID`.
*   **Transaction Inversion Filter:** Isolated and removed **8,905 cancelled orders** (identified by a "C" invoice prefix) to prevent metric distortion.
*   **Pricing Error Clean-up:** Eliminated anomalous records where `UnitPrice <= 0` (system testing records).
*   **Pristine Sandbox:** Reduced the final working dataframe to a verified, highly accurate **406,829 observations**.

### 🧮 Module 02: RFM Feature Engineering
Individual line items were programmatically aggregated by unique `CustomerID` to engineer three core customer metrics:
*   **Recency (R):** Days elapsed between a user's last purchase date and the historical snapshot boundary.
*   **Frequency (F):** Total count of unique invoice orders submitted by that account.
*   **Monetary (M):** Total cumulative financial revenue capital contributed ($Quantity \times UnitPrice$).

### 📊 Module 03: Heuristic Quartile Scoring
Customers were mapped onto a 1-4 scoring matrix based on internal data quantiles. This business layer cleanly categorized users into baseline operational tiers:
*   🥇 **VIP Champions:** High-frequency, high-value spenders who purchased recently.
*   🥈 **Active Casuals:** Moderate purchasing rhythm; stable spenders.
*   ⚠️ **At-Risk / Churn:** High monetary history but haven't purchased in multiple quarters.

### 🤖 Module 04: Unsupervised Machine Learning (K-Means)
To bypass arbitrary heuristic boundaries, a non-parametric **K-Means Clustering** algorithm was trained across the feature space:
*   **Outlier Mitigation:** Handled extreme transaction "whales" (e.g., individual buyers spending over $280,000) using a logarithmic base-10 transformation to stabilize spatial scaling without data loss.
*   **The Elbow Method Optimization:** Ran multiple iteration loops to evaluate feature space inertia. The optimal clustering boundary was mathematically located at **K=3**.

---

## 🛠️ Tech Stack & Tooling
*   **Data Processing & Engineering:** Python, Pandas, NumPy, OpenPyXL
*   **Machine Learning:** Scikit-Learn (`StandardScaler`, `KMeans`)
*   **Visual Explorations:** Matplotlib, Seaborn
*   **Business Intelligence:** Microsoft Power BI Desktop (Custom DAX switch mappings)
