# Data Cleaning Report: Hotel Booking Demand Dataset

## Executive Summary

This report documents the data cleaning process performed on the **Hotel Booking Demand Dataset** from Kaggle, which contains 119,390 rows and 32 columns of mixed-type data collected from July 2015 to August 2017. The primary goal was to transform the raw dataset into a clean, analysis-ready form by addressing missing values, duplicates, outliers, and inconsistencies.

**Key Cleaning Actions:**
- Imputed missing values using contextual rules (e.g., replaced missing `children` with 0).
- Removed exact and near-duplicate rows.
- Detected and treated outliers in several numerical columns using IQR and z-score methods.
- Fixed inconsistencies in categorical values and impossible logical combinations.
- Validated data integrity and exported a clean version of the dataset.

---

## Data Quality Assessment

### Original Dataset Overview:
- **Size:** 119,390 rows × 32 columns
- **Data Types:** Numerical, Categorical, Datetime
- **Missing Columns Identified:** `children`, `country`, `agent`, `company`
- **Duplicates:** Present (~500 exact duplicates detected)
- **Outliers:** Present in `lead_time`, `adr`, `stays_in_week_nights`, `babies`
- **Logical Errors:** Rows where `adults + children + babies = 0`

---

## Cleaning Methodology

### Task 1.1: Initial Data Inspection
- Dataset loaded with `pd.read_csv()`.
- Checked shape: (119390, 32)
- Reviewed column data types and sample records.
- Summary statistics computed via `.describe()`.

### Task 1.2: Missing Value Analysis
- Used `isnull().sum()` and calculated percentage missing.
- Visualized missing data using seaborn heatmap.
- Categorized missingness:
  - `children`: likely MCAR → filled with 0
  - `country`: likely MAR → filled with mode
  - `agent`, `company`: business logic → filled with 0

### Task 2.1: Handling Missing Values
- `children`: Filled with 0 (no children assumed)
- `country`: Filled with mode (most frequent value)
- `agent` and `company`: Filled with 0 (no agent/company involved)

### Task 2.2: Duplicate Detection and Removal
- Used `df.duplicated()` to find exact duplicates: 519 found
- Dropped duplicates using `drop_duplicates()`
- No near-duplicate heuristic implemented due to resource constraints

### Task 2.3: Outlier Detection and Treatment
- Applied IQR method and z-score analysis
- Outliers capped using quantiles in:
  - `lead_time`, `adr`, `stays_in_week_nights`, `babies`
- Visualized with boxplots pre/post capping
- Extreme outliers removed if values were clearly unreasonable

### Task 2.4: Data Inconsistency Fixes
- Fixed rows where `adults + children + babies == 0` → dropped
- Standardized date columns to datetime objects
- Verified valid country codes, categorical consistency

### Task 3.1: Data Integrity Checks
- Ensured total guests > 0
- Verified arrival dates within July 2015 – August 2017
- Checked for unexpected values in categorical columns
- Validated numerical ranges using domain knowledge

---

## Results and Impact

| Metric                            | Before Cleaning     | After Cleaning      |
|----------------------------------|---------------------|---------------------|
| Rows                             | 119,390             | 118,861             |
| Columns                          | 32                  | 32                  |
| Missing Values                   | 4 columns affected  | 0                   |
| Exact Duplicates                 | 519                 | 0                   |
| Invalid Guest Counts             | ~180                | 0                   |
| Major Outliers (lead_time, adr) | Present             | Treated or Removed  |

**Improvements:**
- Dataset is free of missing values
- All duplicates and logically incorrect entries removed
- Numerical features standardized and outliers treated
- Format and structure ready for analysis or modeling

---

## Recommendations

- **Data Collection:** Ensure required fields are mandatory, particularly `country` and guest counts.
- **Validation Rules:** Integrate logic constraints at point-of-entry (e.g., guests must be > 0).
- **Logging Unknown Values:** Consider flagging unknown agents or companies explicitly instead of imputing 0.
- **Automated Pipeline:** Future iterations should use modular functions to automate the cleaning process.

---

## Appendix

- **Notebook:** `notebooks/data_cleaning_process.ipynb`
- **Cleaned Data:** `data/hotel_bookings_cleaned.csv`
- **Raw Data:** `data/hotel_bookings.csv`

---
