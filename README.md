# 📦 Datasets

The single, central collection of datasets for the [📘 Statistical Machine Learning for Noob](https://github.com/mdnuruzzamanKALLOL/Statistical-Machine-Learning-Foundation) series and general ML practice — **418 files, ~331 MB**, combining a personal collection built up over time with a freshly load-tested curated set.

## 📁 Structure

```
Datasets/
├── personal_collection/   ← 206 files — pre-existing personal dataset collection (R/Kaggle/course sources)
├── sklearn/                ← 8 files  — scikit-learn built-in/fetchable datasets
├── seaborn/                ← 22 files — seaborn built-in datasets
├── openml/                 ← 99 files — OpenML real-world datasets (live-verified)
├── synthetic/               ← 83 files — sklearn.datasets.make_* generated datasets
├── misc/
│   ├── text_and_nlp/       ← 29 files — text corpora, stopword lists, word dictionaries (NOT tabular ML data)
│   └── scripts/             ← 1 file   — R data-prep script
├── MANIFEST_curated.csv     ← index of all 212 curated files (name, task, rows, cols, size, source)
├── MANIFEST_personal_collection.csv  ← index of all 206 personal_collection files (name, extension, size)
└── LICENSE                  (MIT)
```

## 🗂️ Two Collections, One Repo

**`personal_collection/`** — an organically grown collection from courses, tutorials, and projects over time (R package datasets like `Cars93`, `Carseats`, `Hitters`, `Prestige`; Kaggle-style sets like `Churn_Modelling`, `Mall_Customers_Int`, `Cust_Segmentation`; time series like `AirPassengers`, `daily-min-temperatures`; and more). Kept exactly as collected — filenames and formats vary (`.csv`, `.tsv`, `.xlsx`, `.rds`, `.json`), since this reflects real, messy, real-world data sourcing.

**`sklearn/` `seaborn/` `openml/` `synthetic/`** — the curated set: every file name-verified live against its source API, every large dataset downsampled to ≤15,000 rows for portability, every synthetic dataset reproducible via `random_state=42`. See [`MANIFEST_curated.csv`](MANIFEST_curated.csv) for the full index, or **[CATALOG.md](CATALOG.md)** for per-dataset task descriptions, API-based load code, and a "which dataset for which ML topic" mapping.

## 🧹 Cleanup Notes (done while consolidating)

- **4 exact byte-duplicate files removed**: `Iris (2).csv` (dup of `iris_code.csv`), `olist_orders_45d.csv` (dup of `orders_45d.csv`), `supermarket_sales - Sheet1.xls` (dup of `supermarket_sales.csv`), `whitewines.csv` (dup of `winequality-white.csv`). Nothing was lost — git history still has them if ever needed.
- **✅ Two mislabels investigated and resolved (2026-07-03):** `cardox.csv` and `oxygen.csv` were byte-identical, and `Ionosphere.csv`/`PimaIndiansDiabetes.csv`/`PimaIndiansDiabetes.rds` were all byte-identical, despite being unrelated dataset names. Content inspection confirmed `cardox.csv` (Mauna Loa CO2 record, `date,value` from 1958) and `Ionosphere.csv` (UCI Ionosphere, 34 `V`-columns + `Class`) were correctly named — the other file in each pair had never actually held its own data, just an accidental copy from the original save. Fix applied: `oxygen.csv` had no recoverable original content, so it was removed rather than guessed at. `PimaIndiansDiabetes.csv` was replaced with the genuine UCI Pima Indians Diabetes dataset (768 rows, fetched from OpenML: `Pregnancies`/`Glucose`/`BloodPressure`/`SkinThickness`/`Insulin`/`BMI`/`DiabetesPedigreeFunction`/`Age`/`Outcome`); the redundant mislabeled `PimaIndiansDiabetes.rds` (also Ionosphere data) was removed since the corrected `.csv` now covers this dataset.
- **29 non-tabular text/NLP files quarantined** to `misc/text_and_nlp/` — these are prose text (e.g. `sachin.txt`, `narendra modi.txt`, `yoga.txt`) and word/stopword lists (`en`, `en-basic`, `stopwords_en.txt`), not structured ML datasets. Kept for any future NLP work, just out of the way of tabular ML practice.
- **1 R script** (`datasets_prep.R`) moved to `misc/scripts/`.

## 🚀 Usage

```python
import pandas as pd

# Personal collection (as originally formatted)
df = pd.read_csv("personal_collection/BostonHousing.csv")

# Curated set (consistent schema: feature_0..feature_n + target/cluster column)
df = pd.read_csv("openml/credit-g.csv")

# Full curated index
manifest = pd.read_csv("MANIFEST_curated.csv")
```

## 🔗 Related

- [**CATALOG.md**](CATALOG.md) — full dataset catalog: task descriptions, API load code, "which dataset for which topic" mapping
- [Statistical Machine Learning for Noob — Foundation](https://github.com/mdnuruzzamanKALLOL/Statistical-Machine-Learning-Foundation)
- [Statistical Machine Learning for Noob — Classical ML](https://github.com/mdnuruzzamanKALLOL/Statistical-Machine-Learning-Classical-ML)

<!-- page-views-badge -->
<div align="center" style="margin-top: 16px;">

![Page Views](https://visitor-badge.laobi.icu/badge?page_id=mdnuruzzamanKALLOL.Datasets.root&left_color=%23FF6F00&right_color=%230e75b6&left_text=Page%20Views)

</div>
