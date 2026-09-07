# 📊 Scalable Customer Segmentation & Financial Decision Support Pipeline
### *Handling 1 Million Customer Records for Wealth Management & Hybrid Financial Services*

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Polars](https://img.shields.io/badge/Polars-Fast%20Dataframe-CD7F32?style=for-the-badge&logo=python&logoColor=white)](https://pola.rs/)
[![DuckDB](https://img.shields.io/badge/DuckDB-OLAP%20DB-FFF000?style=for-the-badge&logo=duckdb&logoColor=black)](https://duckdb.org/)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-ML%20Clustering-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![PowerBI](https://img.shields.io/badge/Power_BI-Dashboard-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Streamlit](https://img.shields.io/badge/Streamlit-App-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)](https://streamlit.io/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

---

## 📌 Executive Summary

Modern retail wealth management faces a double challenge: processing large-scale customer transaction/survey datasets efficiently while converting passive high-net-worth liquidity into active Assets Under Management (AUM).

This project delivers an end-to-end Data Engineering, Data Science, and Data Analytics pipeline built on **1 Million synthetic customer records** (modeled from real-world securities market survey distributions). 

### Key Business Metrics Achieved
- **Processing Time Reduced:** From **~48 seconds** (Pandas in-memory) to **1.4 seconds** (DuckDB + Polars vectorization) across 1M records.
- **Conversion Gap Uncovered:** **89.1%** of potential AUM remains unallocated due to trust/transparency barriers rather than lack of capital.
- **Strategic Impact:** Transformed standard 1D scoring into a **2D Capability–Readiness Matrix**, enabling personalized advisory products and dynamic fee models.

---

## 📐 System Architecture & Workflow

The pipeline seamlessly bridges **Data Engineering (DE)**, **Data Science (DS)**, and **Business Intelligence (DA)**:

```text
┌────────────────────────┐      ┌─────────────────────────┐      ┌──────────────────────────┐
│  Raw Data (1M Rows)    │      │  High-Performance ETL   │      │  Feature Engineering     │
│  - Survey Metrics      │ ───► │  - DuckDB / Polars      │ ───► │  - Capability Score (Y)  │
│  - Demographics & AUM  │      │  - Parquet Columnar Storage    │  - Readiness Score (X)   │
└────────────────────────┘      └─────────────────────────┘      └──────────────────────────┘
                                                                               │
┌────────────────────────┐      ┌─────────────────────────┐                    ▼
│  BI & Decision Support │      │  Advanced ML & Rules    │      ┌──────────────────────────┐
│  - Power BI Dashboard  │ ◄─── │  - K-Means & PCA (2D)   │ ◄─── │  Segmentation Engine     │
│  - Streamlit App       │      │  - Rule-Based Matrix    │      │  - 5 Strategic Segments  │
└────────────────────────┘      └─────────────────────────┘      └──────────────────────────┘

```

---

## 🎯 2D Capability–Readiness Framework

Rather than lumping investment propensity into a single score (which penalizes risk-averse yet wealthy clients), we evaluate clients across two independent axes:

$$\text{Financial Capability } (Y) = 0.6 \times \text{FHS} + 0.4 \times \text{ICS}$$

$$\text{Conversion Readiness } (X) = 0.6 \times \text{CRS} + 0.4 \times \text{ANS}$$

* **FHS (Financial Health Score):** Balance sheet strength & liquidity.
* **ICS (Investment Knowledge Score):** Product understanding & financial literacy.
* **CRS (Commercial Readiness Score):** Fee commitment & willingness to invest.
* **ANS (Advisory Need Score):** Financial gap & necessity for external guidance.

### Segment Breakdown Matrix

| Segment Name | Y (Capability) | X (Readiness) | Primary Business Action | Target Fee Structure |
| --- | --- | --- | --- | --- |
| **High-Priority (Khách hàng Ưu tiên)** | $\ge 3.5$ | $\ge 3.5$ | High-touch VIP Advisory & Capital Allocation | Performance-linked / Tiered AUM Fee |
| **Self-Directed Wealth (Tự chủ đầu tư)** | $\ge 3.5$ | $< 3.5$ | Decision-support tools, full transparency | Fee-for-service / Performance fee |
| **High-Intent / Low-Capital** | $< 3.5$ | $\ge 3.5$ | Low-margin automated advisory / Micro-investing | Free basic / Premium advisory |
| **Nurturing (Nuôi dưỡng)** | $< 3.5$ | $< 3.5$* | Financial literacy, educational campaigns | Zero-fee onboarding |
| **Low Potential** | $< 3.5$ | $< 3.5$ | Automated retention / Zero sales effort | Standard execution fee |

**Satisfies $ICS \ge 3.0$ or Age $\le 35$.*

---

## ⚡ Data Engineering & Benchmark Results

To handle **1,000,000 records** efficiently without Out-Of-Memory (OOM) issues:

* **Storage Optimization:** CSV raw files (~280MB) converted to **Apache Parquet** (~42MB, 85% compression).
* **Execution Benchmark (1M Records Transformation):**

| Framework | Processing Time | Memory Peak | Parallelization |
| --- | --- | --- | --- |
| Pandas (In-Memory) | ~48.2s | ~1.8 GB | Single-Core |
| **Polars (LazyFrame)** | **1.8s** | **~380 MB** | Multi-Threaded |
| **DuckDB (In-Process SQL)** | **1.4s** | **~210 MB** | Vectorized Execution |

---

## 💡 Key Business Insights

1. **The AUM Paradox:** High-net-worth clients ("Self-Directed") hold >50% of idle assets but contribute low fee revenue because they demand **transparency and control**, rejecting traditional opaque management fees.
2. **Fee Preference Shift:** 68% of surveyed investors prefer **Performance-based fees** or **Freemium advisory** over fixed monthly retainer fees.
3. **Age & Lifecycle Dynamics:**
* **Under 35:** Knowledge-hungry, low current capital. Require automated savings & robo-advisory.
* **36–55:** High cash flow & debt obligations. Require growth portfolios & automated execution.
* **Over 55:** Wealth preservation focus. Require capital protection & structured yield products.



---

## 📂 Repository Structure

```text
├── assets/                    # Screenshots, architecture diagrams, charts
│   ├── dashboard_overview.png
│   └── matrix_segmentation.png
├── data/                      # Synthetic data samples (NO proprietary data)
│   ├── raw_sample.csv
│   └── processed_sample.parquet
├── docs/                      # Full report PDF & Presentation Slides
│   └── Internship_Final_Report.pdf
├── notebooks/                 # Exploratory & Model Testing
│   ├── 01_data_cleaning_polars.ipynb
│   ├── 02_segmentation_rules_vs_kmeans.ipynb
│   └── 03_pca_feature_reduction.ipynb
├── src/                       # Production Code Pipeline
│   ├── etl_duckdb.py          # Data pipeline script
│   ├── segmentation_engine.py # Rule-based & ML clustering engine
│   └── app.py                 # Streamlit interactive application
├── .gitignore
├── README.md
└── requirements.txt

```

---

## 🚀 Quick Start & Installation

1. **Clone the repository:**
```bash
git clone [https://github.com/your-username/scalable-customer-segmentation.git](https://github.com/your-username/scalable-customer-segmentation.git)
cd scalable-customer-segmentation

```


2. **Set up Virtual Environment:**
```bash
python -m venv venv
source venv/bin/activate  # On Windows use: venv\\Scripts\\activate
pip install -r requirements.txt

```


3. **Run Data ETL Pipeline (DuckDB & Polars):**
```bash
python src/etl_duckdb.py

```


4. **Launch Streamlit Interactive Dashboard:**
```bash
streamlit run src/app.py

```



---

## 👤 Author & Acknowledgments

* **Developer:** Nguyễn Thái Thanh Vân
* **Role:** Data Analyst Intern / Data Science Student
* **Domain:** Business Data Science & Wealth Management Analytics

---

*Disclaimer: All datasets used in this repository are synthetic/masked to comply with privacy and NDA regulations.*
"""

with open("README.md", "w", encoding="utf-8") as f:
f.write(markdown_content)

print("FILE_GENERATED: README.md")

```

```text?code_stdout&code_event_index=1
FILE_GENERATED: README.md


```

Dưới đây là mẫu file `README.md` đã được biên soạn và tối ưu hóa chuẩn Markdown dành riêng cho GitHub Repo của bạn.

File này đã được tích hợp đầy đủ các **badge trang trí chuyên nghiệp** (Python, Polars, DuckDB, Power BI, Streamlit...), trình bày chuẩn mực theo mô hình 3 trụ cột **DE + DS + DA** trên tập dữ liệu 1 triệu dòng và công thức phân cụm 2 chiều.

File `README.md` chuẩn đã được khởi tạo sẵn:


---

### 📝 Mã nguồn Markdown (Bạn có thể sao chép trực tiếp vào GitHub)

```markdown
# 📊 Scalable Customer Segmentation & Financial Decision Support Pipeline
### *Handling 1 Million Customer Records for Wealth Management & Hybrid Financial Services*

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Polars](https://img.shields.io/badge/Polars-Fast%20Dataframe-CD7F32?style=for-the-badge&logo=python&logoColor=white)](https://pola.rs/)
[![DuckDB](https://img.shields.io/badge/DuckDB-OLAP%20DB-FFF000?style=for-the-badge&logo=duckdb&logoColor=black)](https://duckdb.org/)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-ML%20Clustering-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![PowerBI](https://img.shields.io/badge/Power_BI-Dashboard-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Streamlit](https://img.shields.io/badge/Streamlit-App-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)](https://streamlit.io/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

---

## 📌 Executive Summary

Modern retail wealth management faces a double challenge: processing large-scale customer transaction/survey datasets efficiently while converting passive high-net-worth liquidity into active Assets Under Management (AUM).

This project delivers an end-to-end Data Engineering, Data Science, and Data Analytics pipeline built on **1 Million synthetic customer records** (modeled from real-world securities market survey distributions). 

### Key Business Metrics Achieved
- **Processing Time Reduced:** From **~48 seconds** (Pandas in-memory) to **1.4 seconds** (DuckDB + Polars vectorization) across 1M records.
- **Conversion Gap Uncovered:** **89.1%** of potential AUM remains unallocated due to trust/transparency barriers rather than lack of capital.
- **Strategic Impact:** Transformed standard 1D scoring into a **2D Capability–Readiness Matrix**, enabling personalized advisory products and dynamic fee models.

---

## 📐 System Architecture & Workflow

The pipeline seamlessly bridges **Data Engineering (DE)**, **Data Science (DS)**, and **Business Intelligence (DA)**:

```text
┌────────────────────────┐      ┌─────────────────────────┐      ┌──────────────────────────┐
│  Raw Data (1M Rows)    │      │  High-Performance ETL   │      │  Feature Engineering     │
│  - Survey Metrics      │ ───► │  - DuckDB / Polars      │ ───► │  - Capability Score (Y)  │
│  - Demographics & AUM  │      │  - Parquet Columnar Storage    │  - Readiness Score (X)   │
└────────────────────────┘      └─────────────────────────┘      └──────────────────────────┘
                                                                               │
┌────────────────────────┐      ┌─────────────────────────┐                    ▼
│  BI & Decision Support │      │  Advanced ML & Rules    │      ┌──────────────────────────┐
│  - Power BI Dashboard  │ ◄─── │  - K-Means & PCA (2D)   │ ◄─── │  Segmentation Engine     │
│  - Streamlit App       │      │  - Rule-Based Matrix    │      │  - 5 Strategic Segments  │
└────────────────────────┘      └─────────────────────────┘      └──────────────────────────┘

```

---

## 🎯 2D Capability–Readiness Framework

Rather than lumping investment propensity into a single score (which penalizes risk-averse yet wealthy clients), we evaluate clients across two independent axes:

$$\text{Financial Capability } (Y) = 0.6 \times \text{FHS} + 0.4 \times \text{ICS}$$

$$\text{Conversion Readiness } (X) = 0.6 \times \text{CRS} + 0.4 \times \text{ANS}$$

* **FHS (Financial Health Score):** Balance sheet strength & liquidity.
* **ICS (Investment Knowledge Score):** Product understanding & financial literacy.
* **CRS (Commercial Readiness Score):** Fee commitment & willingness to invest.
* **ANS (Advisory Need Score):** Financial gap & necessity for external guidance.

### Segment Breakdown Matrix

| Segment Name | Y (Capability) | X (Readiness) | Primary Business Action | Target Fee Structure |
| --- | --- | --- | --- | --- |
| **High-Priority (Khách hàng Ưu tiên)** | $\ge 3.5$ | $\ge 3.5$ | High-touch VIP Advisory & Capital Allocation | Performance-linked / Tiered AUM Fee |
| **Self-Directed Wealth (Tự chủ đầu tư)** | $\ge 3.5$ | $< 3.5$ | Decision-support tools, full transparency | Fee-for-service / Performance fee |
| **High-Intent / Low-Capital** | $< 3.5$ | $\ge 3.5$ | Low-margin automated advisory / Micro-investing | Free basic / Premium advisory |
| **Nurturing (Nuôi dưỡng)** | $< 3.5$ | $< 3.5$* | Financial literacy, educational campaigns | Zero-fee onboarding |
| **Low Potential** | $< 3.5$ | $< 3.5$ | Automated retention / Zero sales effort | Standard execution fee |

**Satisfies $ICS \ge 3.0$ or Age $\le 35$.*

---

## ⚡ Data Engineering & Benchmark Results

To handle **1,000,000 records** efficiently without Out-Of-Memory (OOM) issues:

* **Storage Optimization:** CSV raw files (~280MB) converted to **Apache Parquet** (~42MB, 85% compression).
* **Execution Benchmark (1M Records Transformation):**

| Framework | Processing Time | Memory Peak | Parallelization |
| --- | --- | --- | --- |
| Pandas (In-Memory) | ~48.2s | ~1.8 GB | Single-Core |
| **Polars (LazyFrame)** | **1.8s** | **~380 MB** | Multi-Threaded |
| **DuckDB (In-Process SQL)** | **1.4s** | **~210 MB** | Vectorized Execution |

---

## 💡 Key Business Insights

1. **The AUM Paradox:** High-net-worth clients ("Self-Directed") hold >50% of idle assets but contribute low fee revenue because they demand **transparency and control**, rejecting traditional opaque management fees.
2. **Fee Preference Shift:** 68% of surveyed investors prefer **Performance-based fees** or **Freemium advisory** over fixed monthly retainer fees.
3. **Age & Lifecycle Dynamics:**
* **Under 35:** Knowledge-hungry, low current capital. Require automated savings & robo-advisory.
* **36–55:** High cash flow & debt obligations. Require growth portfolios & automated execution.
* **Over 55:** Wealth preservation focus. Require capital protection & structured yield products.



---

## 📂 Repository Structure

```text
├── assets/                    # Screenshots, architecture diagrams, charts
│   ├── dashboard_overview.png
│   └── matrix_segmentation.png
├── data/                      # Synthetic data samples (NO proprietary data)
│   ├── raw_sample.csv
│   └── processed_sample.parquet
├── docs/                      # Full report PDF & Presentation Slides
│   └── Internship_Final_Report.pdf
├── notebooks/                 # Exploratory & Model Testing
│   ├── 01_data_cleaning_polars.ipynb
│   ├── 02_segmentation_rules_vs_kmeans.ipynb
│   └── 03_pca_feature_reduction.ipynb
├── src/                       # Production Code Pipeline
│   ├── etl_duckdb.py          # Data pipeline script
│   ├── segmentation_engine.py # Rule-based & ML clustering engine
│   └── app.py                 # Streamlit interactive application
├── .gitignore
├── README.md
└── requirements.txt

```

---

## 🚀 Quick Start & Installation

1. **Clone the repository:**
```bash
git clone [https://github.com/your-username/scalable-customer-segmentation.git](https://github.com/your-username/scalable-customer-segmentation.git)
cd scalable-customer-segmentation

```


2. **Set up Virtual Environment:**
```bash
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate
pip install -r requirements.txt

```


3. **Run Data ETL Pipeline (DuckDB & Polars):**
```bash
python src/etl_duckdb.py

```


4. **Launch Streamlit Interactive Dashboard:**
```bash
streamlit run src/app.py

```



---

## 👤 Author & Acknowledgments

* **Developer:** Nguyễn Thái Thanh Vân
* **Role:** Data Analyst Intern / Data Science Student
* **Domain:** Business Data Science & Wealth Management Analytics

---

*Disclaimer: All datasets used in this repository are synthetic/masked to comply with privacy and NDA regulations.*

```

```
