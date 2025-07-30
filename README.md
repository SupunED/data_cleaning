# 🧹 Hotel Booking Demand – Data Cleaning Project

This project focuses on cleaning the [Hotel Booking Demand Dataset](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand) to prepare it for analysis.

## 📌 Objectives

- Handle missing values using contextual imputation
- Detect and remove duplicates
- Identify and treat outliers in numerical features
- Fix inconsistent formats and logical errors
- Validate data integrity and consistency

## 📁 Project Structure

```text
hotel-data-cleaning/
├── data/
│   ├── hotel_bookings.csv           # Original dataset
│   └── hotel_bookings_cleaned.csv   # Cleaned dataset
├── notebooks/
│   └── data_cleaning_process.ipynb  # Jupyter notebook with full process
├── reports/
│   └── data_cleaning_report.md      # Full markdown report

```


## ✅ Key Outcomes

- ~500 duplicate records removed
- Missing values in 4 key columns handled
- Outliers treated using IQR and z-score methods
- All guest entries validated (`adults + children + babies > 0`)
- Clean, analysis-ready dataset exported

## 🔗 Dependencies

```bash
pip install pandas numpy matplotlib seaborn

```
