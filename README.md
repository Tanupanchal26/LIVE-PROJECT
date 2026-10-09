# Rossmann Store Sales Forecasting

A machine learning project to predict daily sales for Rossmann retail stores using historical sales data, store information, promotions, and holiday indicators.

---

## Business Problem

Retail stores need accurate sales forecasts to make better decisions around inventory, staffing, and operations. Inaccurate forecasting leads to excess stock, product shortages, and wasted resources.

This project uses the [Rossmann Store Sales dataset](https://www.kaggle.com/c/rossmann-store-sales) to build a forecasting system that predicts daily sales for individual stores based on historical patterns, promotions, store characteristics, and calendar features.

---

## Project Objectives

- Predict daily sales for individual Rossmann stores.
- Analyse historical sales trends and weekly patterns.
- Understand the relationship between promotions, holidays, and sales.
- Identify useful store characteristics for forecasting.
- Support better inventory and operational planning.

For full business requirements, see [docs/BRD.md](docs/BRD.md).

---

## Datasets

All three datasets are sourced from the Kaggle Rossmann Store Sales competition. They are **not included in this repository** (excluded via `.gitignore`).

| File | Description |
|---|---|
| `data/train.csv` | Historical daily sales per store (Jan 2013 – Jul 2015) |
| `data/store.csv` | Store-level metadata: type, assortment, competition, promotions |
| `data/test.csv` | Store and date records requiring sales predictions |

### Key Columns

**train.csv** — `Store`, `DayOfWeek`, `Date`, `Sales`, `Customers`, `Open`, `Promo`, `StateHoliday`, `SchoolHoliday`

**store.csv** — `Store`, `StoreType`, `Assortment`, `CompetitionDistance`, `Promo2`, `PromoInterval`

---

## Project Folder Structure

```
Rossmann-Project/
├── data/                   # Raw datasets (not committed to Git)
│   ├── train.csv
│   ├── store.csv
│   ├── test.csv
│   └── rossmann_cleaned.csv
├── docs/
│   └── BRD.md              # Business Requirements Document
├── notebooks/
│   └── rossmann_eda.ipynb  # Main EDA and preprocessing notebook
└── .gitignore
```

---

## Technologies Used

- Python 3.11
- Jupyter Notebook
- pandas, NumPy
- Matplotlib, Seaborn
- scikit-learn
- Git and GitHub

---

## Work Completed

### 1. Project Setup
- Created the project folder structure.
- Configured `.gitignore` to exclude datasets, virtual environments, and cache files.
- Started project documentation (`docs/BRD.md`).

### 2. Data Loading
Loaded all three datasets from `../data/` using relative paths:

```python
train = pd.read_csv("../data/train.csv")
store = pd.read_csv("../data/store.csv")
test  = pd.read_csv("../data/test.csv")
```

Dataset shapes confirmed:
- `train.csv` — 1,017,209 rows × 9 columns
- `store.csv` — 1,115 rows × 10 columns
- `test.csv` — 41,088 rows × 8 columns

### 3. Data Inspection
- Reviewed column names, data types, and value counts.
- Identified missing values across all three datasets.
- Confirmed the training date range: **1 January 2013 to 31 July 2015**.

### 4. Data Preprocessing
- Converted the `Date` column in `train.csv` and `test.csv` to `datetime` format.
- Merged `train.csv` with `store.csv` on the `Store` column.
- Merged dataset shape: **1,017,209 rows × 18 columns**.

### 5. Exploratory Data Analysis (EDA)
The following analyses were performed in `notebooks/rossmann_eda.ipynb`:

- **Sales distribution** — histogram of daily sales values.
- **Sales over time** — trend of total sales across the full date range.
- **Day-of-week patterns** — average sales by day of the week.
- **Promotions** — comparison of sales on promo vs. non-promo days.
- **Store open/closed status** — effect of the `Open` flag on sales.
- **Holidays** — sales behaviour on state holidays and school holidays.
- **Store types** — sales comparison across store types (A, B, C, D).
- **Assortment levels** — sales by assortment category (a, b, c).
- **Competition distance** — relationship between nearby competition and sales.

### 6. Chronological Data Split
To avoid data leakage, the labeled data was split by date:

| Split | Period | Purpose |
|---|---|---|
| Training | Before 1 June 2015 | Model training |
| Validation | June 2015 | Hyperparameter tuning |
| Evaluation | July 2015 | Final performance assessment |

The original `test.csv` is kept separate for generating final competition predictions.



## Documentation

- [Business Requirements Document (BRD)](docs/BRD.md)

---

## Author

**Tanya Panchal**
GitHub: [https://github.com/Tanupanchal26](https://github.com/Tanupanchal26)
