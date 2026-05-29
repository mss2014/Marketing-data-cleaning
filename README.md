# Marketing-data-cleaning
A comprehensive data preprocessing and cleaning project focused on restructuring marketing campaign datasets. Features step-by-step implementations for handling missing values, standardizing formats, and correcting data types using both Python (Pandas) and Microsoft Excel.
# Marketing Campaign Data Cleaning & Preprocessing Hub

A comprehensive, end-to-end data cleaning and preprocessing project featuring standard data manipulation workflows. This repository demonstrates how to take raw, messy marketing analytics data (`marketing_campaign.csv`) and transform it into a pristine, analysis-ready format (`cleaned_marketing_campaign.csv`) using two distinct methodologies: **Python (Pandas)** and **Microsoft Excel**.

---

## 📌 Project Overview

Data preparation consumes up to 80% of a data analyst's time. The objective of this project is to build a reliable pipeline that handles real-world data anomalies—such as missing values, inconsistent text formatting, invalid data categories, and structural header errors—to ensure robust downstream reporting and data modeling.

### Core Enhancements Applied:
1. **Header Uniformity:** Standardized all column labels to lower_snake_case (e.g., `Year_Birth` $\rightarrow$ `year_birth`) for consistent code and query compilation.
2. **Missing Value Imputation:** Detected and handled 24 missing records in the `income` column using robust statistical metrics to avoid data loss.
3. **Categorical Consolidation:** Cleaned and regularized high-variance categorical entries (`education` and `marital_status`), removing trailing whitespaces and aligning non-standard classifications.
4. **Data Type Correction:** Converted date metrics explicitly into a unified `dd-mm-yyyy` datetime scheme and validated appropriate structural types (integers vs. floats).
5. **Deduplication:** Audited the dataset for redundant rows to enforce strict row-level uniqueness.

---

## 🛠️ Implementation Pipelines

Automated Pipeline via Python (Pandas)

The data cleaning pipeline is automated within `clean_data.py`. Run the script to ingest the raw file and output the cleaned version seamlessly.

```python
import pandas as pd

# 1. Ingest raw tab-separated marketing data
df = pd.read_csv('marketing_campaign.csv', sep='\t')

# 2. Enforce clean, uniform snake_case headers
df.columns = df.columns.str.lower().str.strip().str.replace(' ', '_')

# 3. Impute missing numeric records using the column median
income_median = df['income'].median()
df['income'] = df['income'].fillna(income_median)

# 4. Filter out duplicate records
df = df.drop_duplicates()

# 5. Standardize categorical text attributes
df['education'] = df['education'].str.lower().str.strip()
df['marital_status'] = df['marital_status'].str.lower().str.strip()
df['marital_status'] = df['marital_status'].replace({'alone': 'single', 'yolo': 'single', 'absurd': 'single'})

# 6. Parse date strings into standardized datetime types
df['dt_customer'] = pd.to_datetime(df['dt_customer'], format='%d-%m-%Y')

# 7. Export production-ready dataset
df.to_csv('cleaned_marketing_campaign.csv', index=False, date_format='%d-%m-%Y')
print("Data pipeline executed successfully! Saved as 'cleaned_marketing_campaign.csv'.")

---

├── marketing_campaign.csv          # Raw, untouched input dataset
├── cleaned_marketing_campaign.csv  # Final, processed output dataset
└── README.md                       # Documentation and project walkthrough

---

## License
This project is licensed under the MIT License. See the `LICENSE` file for more details.
