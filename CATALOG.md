# 📦 Dataset Catalog — 162 Cataloged Datasets, 212 as Ready-to-Use CSV

A curated, **fully load-tested** catalog of datasets for practicing every algorithm in the [📘 Statistical Machine Learning for Noob](https://github.com/mdnuruzzamanKALLOL/Statistical-Machine-Learning-Foundation) series (Foundation + [Classical ML](https://github.com/mdnuruzzamanKALLOL/Statistical-Machine-Learning-Classical-ML)). Every dataset below has **both** a one-line API load call **and** an actual CSV file in this repo — pick whichever fits your workflow.

## 💾 Local CSV Files

All 212 curated datasets live right here, organized as [`sklearn/`](sklearn/), [`seaborn/`](seaborn/), [`openml/`](openml/), [`synthetic/`](synthetic/), indexed in [`MANIFEST_curated.csv`](MANIFEST_curated.csv). This author's broader personal dataset collection (206 more files) lives in [`personal_collection/`](personal_collection/) — see the main [README.md](README.md) for the full repo structure.

```python
import pandas as pd
df = pd.read_csv("openml/credit-g.csv")          # any dataset, offline, no network call
manifest = pd.read_csv("MANIFEST_curated.csv")    # full searchable index of all 212 curated files
```

## 📊 Catalog Summary

| Source | Cataloged | As CSV | Best for |
|---|---|---|---|
| [scikit-learn built-in / fetchable](#-1-scikit-learn-built-in--fetchable-13) | 13 | 8 (5 are text/image, kept API-only) | Classic benchmarks, zero setup |
| [Seaborn built-in](#-2-seaborn-built-in-22) | 22 | 22 | EDA practice, quick visualization datasets |
| [OpenML — batch 1](#-3-openml-real-world-batch-1-30) | 30 | 30 | Classification-heavy real-world practice |
| [OpenML — batch 2](#-4-openml-real-world-batch-2-21) | 21 | 21 | More classification + a few regression |
| [OpenML — batch 3](#-5-openml-real-world-batch-3-48) | 48 | 48 | Extra real-world variety (medical, sensor, economic data) |
| [Synthetic generators](#-6-synthetic-generators-sklearndatasetsmake_-83) | 28 (+55 extra param sweeps as CSV only) | 83 | Algorithm-targeted practice (clustering, manifolds, imbalanced classes...) |
| **Total** | **162 cataloged** | **212 CSV files (~53 MB)** | |

Datasets larger than 15,000 rows (California Housing, Covertype, Adult, Diamonds, Letter, and several OpenML sets) were **randomly downsampled to 15,000 rows** (`random_state=42`) to keep individual files small — check the `sampled_from` column in `MANIFEST_curated.csv` for the original row count, or use the API load call below to get the full, un-sampled version.

## 📑 Table of Contents

1. [How to Use This Catalog](#-how-to-use-this-catalog)
2. [1. scikit-learn Built-in / Fetchable (13)](#-1-scikit-learn-built-in--fetchable-13)
3. [2. Seaborn Built-in (22)](#-2-seaborn-built-in-22)
4. [3. OpenML Real-World, Batch 1 (30)](#-3-openml-real-world-batch-1-30)
5. [4. OpenML Real-World, Batch 2 (21)](#-4-openml-real-world-batch-2-21)
6. [5. OpenML Real-World, Batch 3 (48)](#-5-openml-real-world-batch-3-48)
7. [6. Synthetic Generators — `sklearn.datasets.make_*` (83)](#-6-synthetic-generators-sklearndatasetsmake_-83)
8. [Which Dataset for Which Topic?](#-which-dataset-for-which-topic)
9. [Caveats & Notes](#️-caveats--notes)

---

## 🚀 How to Use This Catalog

Every dataset resolves to a Pandas DataFrame in one line:

```python
# scikit-learn built-in
from sklearn.datasets import load_iris
df = load_iris(as_frame=True).frame

# seaborn built-in
import seaborn as sns
df = sns.load_dataset("titanic")

# OpenML (real-world, name-based lookup)
from sklearn.datasets import fetch_openml
df = fetch_openml(name="credit-g", as_frame=True, parser="auto").frame

# synthetic generator
from sklearn.datasets import make_blobs
X, y = make_blobs(n_samples=300, centers=3, random_state=42)
```

First call downloads and caches (`~/scikit_learn_data/`); every call after that is instant and offline.

---

## 🧱 1. scikit-learn Built-in / Fetchable (13)

| # | Name | Task | Load Code | Notes |
|---|---|---|---|---|
| 1 | Iris | Classification (3-class) | `load_iris(as_frame=True).frame` | The "hello world" of ML — 150 rows, 4 features |
| 2 | Wine | Classification (3-class) | `load_wine(as_frame=True).frame` | Chemical analysis of wines from 3 cultivars |
| 3 | Breast Cancer Wisconsin | Classification (binary) | `load_breast_cancer(as_frame=True).frame` | Diagnostic features, malignant vs benign |
| 4 | Diabetes | Regression | `load_diabetes(as_frame=True).frame` | Disease progression one year after baseline |
| 5 | Digits | Classification (10-class) | `load_digits(as_frame=True).frame` | 8×8 handwritten digit images, flattened |
| 6 | Linnerud | Regression (multi-output) | `load_linnerud(as_frame=True).frame` | Exercise vs physiological measurements, tiny (20 rows) |
| 7 | California Housing | Regression | `fetch_california_housing(as_frame=True).frame` | ~20,600 rows, median house value target |
| 8 | Covertype | Classification (7-class, large) | `fetch_covtype(as_frame=True).frame` | ~580,000 rows — good for testing scalability |
| 9 | 20 Newsgroups | Text Classification | `fetch_20newsgroups(subset="train")` | ~18,000 posts, 20 categories |
| 10 | Olivetti Faces | Image Classification | `fetch_olivetti_faces()` | 400 face images, 40 people |
| 11 | LFW People | Image Classification | `fetch_lfw_people(min_faces_per_person=70)` | "Labeled Faces in the Wild" subset |
| 12 | RCV1 | Text Multilabel | `fetch_rcv1()` | Reuters news categorization, large |
| 13 | KDD Cup 99 | Classification (intrusion detection) | `fetch_kddcup99(subset="SA")` | Network intrusion detection benchmark |

---

## 🎨 2. Seaborn Built-in (22)

| # | Name | Suggested Task | Load Code | Notes |
|---|---|---|---|---|
| 14 | tips | Regression (`tip`) | `sns.load_dataset("tips")` | Restaurant tipping, classic Seaborn demo dataset |
| 15 | titanic | Classification (`survived`) | `sns.load_dataset("titanic")` | Different columns than the OpenML version — good for comparing sources |
| 16 | iris | Classification (`species`) | `sns.load_dataset("iris")` | Same flowers, Seaborn-formatted |
| 17 | penguins | Classification (`species`) | `sns.load_dataset("penguins")` | Modern Iris alternative, has real missing values |
| 18 | diamonds | Regression (`price`) | `sns.load_dataset("diamonds")` | ~54,000 rows, great for scaling/EDA practice |
| 19 | mpg | Regression (`mpg`) | `sns.load_dataset("mpg")` | Car fuel efficiency, has missing values |
| 20 | planets | EDA / Regression | `sns.load_dataset("planets")` | Exoplanet discovery methods and masses |
| 21 | flights | Time series / EDA | `sns.load_dataset("flights")` | Monthly airline passengers, classic seasonality demo |
| 22 | exercise | EDA (ANOVA-style) | `sns.load_dataset("exercise")` | Small, good for groupby/categorical practice |
| 23 | anagrams | EDA | `sns.load_dataset("anagrams")` | Tiny experimental dataset |
| 24 | anscombe | EDA — **"always plot your data"** | `sns.load_dataset("anscombe")` | Anscombe's Quartet: 4 datasets, identical stats, wildly different shapes |
| 25 | attention | EDA | `sns.load_dataset("attention")` | Small psychology experiment dataset |
| 26 | brain_networks | EDA (high-dimensional) | `sns.load_dataset("brain_networks")` | 63 columns — good for correlation/PCA practice |
| 27 | car_crashes | Regression | `sns.load_dataset("car_crashes")` | US state-level crash statistics |
| 28 | dots | EDA / time series | `sns.load_dataset("dots")` | Neuroscience-style response-time dataset |
| 29 | dowjones | Time series | `sns.load_dataset("dowjones")` | Historical Dow Jones index |
| 30 | fmri | EDA / time series | `sns.load_dataset("fmri")` | Brain imaging signal over time |
| 31 | geyser | **Clustering** (classic!) | `sns.load_dataset("geyser")` | Old Faithful eruptions — the textbook 2-cluster demo |
| 32 | glue | EDA | `sns.load_dataset("glue")` | NLP benchmark scores |
| 33 | healthexp | Time series / Regression | `sns.load_dataset("healthexp")` | Health expenditure vs life expectancy by country |
| 34 | seaice | Time series / Regression | `sns.load_dataset("seaice")` | Arctic sea ice extent over time |
| 35 | taxis | Classification / Regression | `sns.load_dataset("taxis")` | NYC taxi trips — fare (regression) or payment type (classification) |

---

## 🌍 3. OpenML Real-World, Batch 1 (30)

All loaded via `fetch_openml(name="<name>", as_frame=True, parser="auto").frame`.

| # | Name | Task | Rows | Notes |
|---|---|---|---|---|
| 36 | `titanic` | Classification | 2,201 | OpenML's version — compare against seaborn's |
| 37 | `adult` | Classification (income >$50K) | 48,842 | The classic "Census Income" benchmark |
| 38 | `credit-g` | Classification (credit risk) | 1,000 | German Credit dataset |
| 39 | `mushroom` | Classification (edible/poisonous) | 8,124 | Perfectly separable with the right features |
| 40 | `spambase` | Classification (spam) | 4,601 | Email spam detection, 57 numeric features |
| 41 | `ionosphere` | Classification | 351 | Radar returns, good/bad |
| 42 | `sonar` | Classification (rock/mine) | 208 | Small, high-dimensional (60 features) |
| 43 | `glass` | Classification (6-class) | 214 | Glass type from chemical composition |
| 44 | `ecoli` | Classification (protein localization) | 336 | Multi-class, imbalanced |
| 45 | `yeast` | Classification (protein localization) | 1,484 | 10-class, imbalanced — good for class-imbalance practice |
| 46 | `car` | Classification (car acceptability) | 1,728 | All categorical features — great encoding practice |
| 47 | `zoo` | Classification (animal type) | 101 | Small, mostly binary features |
| 48 | `balance-scale` | Classification | 625 | Simple synthetic-like real dataset, 3-class |
| 49 | `tic-tac-toe` | Classification (win/loss) | 958 | All categorical, non-linear patterns |
| 50 | `vote` | Classification (party) | 435 | Congressional voting records, mostly binary features |
| 51 | `segment` | Classification (7-class) | 2,310 | Image segmentation |
| 52 | `vehicle` | Classification (4-class) | 846 | Silhouette-based vehicle type |
| 53 | `satimage` | Classification (6-class) | 6,430 | Satellite image land cover |
| 54 | `letter` | Classification (26-class) | 20,000 | Letter recognition — big multiclass practice |
| 55 | `abalone` | Regression (age) | 4,177 | Predict age from physical measurements |
| 56 | `kin8nm` | Regression | 8,192 | Robot arm simulation, non-linear |
| 57 | `pol` | Regression | 15,000 | Telecom pricing data |
| 58 | `wine-quality-red` | Regression/Classification (quality) | 1,599 | Ordinal quality score 0-10 |
| 59 | `wine-quality-white` | Regression/Classification (quality) | 4,898 | Larger sibling of red wine version |
| 60 | `phoneme` | Classification (binary) | 5,404 | Speech signal, nasal vs oral |
| 61 | `blood-transfusion-service-center` | Classification (donated) | 748 | Small, clean, binary |
| 62 | `banknote-authentication` | Classification (binary) | 1,372 | Forged vs genuine banknotes, from image wavelets |
| 63 | `seeds` | Classification (3-class) | 210 | Wheat kernel measurements |
| 64 | `climate-model-simulation-crashes` | Classification (binary) | 540 | Simulation crash prediction, imbalanced |
| 65 | `diabetes` | Classification (binary) | 768 | Pima Indians Diabetes — very commonly cited benchmark |

---

## 🌍 4. OpenML Real-World, Batch 2 (21)

Same load pattern: `fetch_openml(name="<name>", as_frame=True, parser="auto").frame`.

| # | Name | Task | Rows | Notes |
|---|---|---|---|---|
| 66 | `monks-problems-1` | Classification | 556 | Classic symbolic-learning benchmark |
| 67 | `hepatitis` | Classification | 155 | Medical, many missing values — good imputation practice |
| 68 | `heart-statlog` | Classification (heart disease) | 270 | Small, clean, widely used |
| 69 | `liver-disorders` | Classification/Regression | 345 | BUPA liver disorders |
| 70 | `haberman` | Classification (survival) | 306 | Breast cancer survival, imbalanced |
| 71 | `page-blocks` | Classification (5-class) | 5,473 | Document layout analysis, very imbalanced |
| 72 | `nursery` | Classification (5-class) | 12,960 | All categorical, large |
| 73 | `kr-vs-kp` | Classification (chess endgame) | 3,196 | King-Rook vs King-Pawn, all categorical |
| 74 | `anneal` | Classification | 898 | Steel annealing, many categorical + missing |
| 75 | `audiology` | Classification (many classes) | 226 | High missingness — good for topic 03 practice |
| 76 | `lymph` | Classification (4-class) | 148 | Small medical dataset |
| 77 | `primary-tumor` | Classification (many classes) | 339 | High missingness, high class count |
| 78 | `breast-w` | Classification (binary) | 699 | Breast Cancer Wisconsin (Original) — compare vs. sklearn's version |
| 79 | `thyroid-allbp` | Classification | 2,800 | Medical, many features |
| 80 | `cmc` | Classification (3-class) | 1,473 | Contraceptive method choice, socioeconomic features |
| 81 | `autos` | Regression (price) | 205 | Car price prediction, mixed types |
| 82 | `credit-approval` | Classification (binary) | 690 | Credit card approval, mixed types + missing |
| 83 | `hill-valley` | Classification (binary) | 1,212 | 100 numeric features from terrain shape |
| 84 | `madelon` | Classification (binary) | 2,600 | NIPS feature-selection benchmark, 500 mostly-noise features |
| 85 | `optdigits` | Classification (10-class) | 5,620 | Optical digit recognition |
| 86 | `pendigits` | Classification (10-class) | 10,992 | Pen-based digit recognition |

---

## 🌍 5. OpenML Real-World, Batch 3 (48)

Same load pattern: `fetch_openml(name="<name>", as_frame=True, parser="auto").frame`. This batch adds economic, sensor, and medical datasets not covered above.

| # | Name | Task | Rows | Notes |
|---|---|---|---|---|
| 87 | `wdbc` | Classification (binary) | 569 | Wisconsin Diagnostic Breast Cancer |
| 88 | `labor` | Classification (binary) | 57 | Labor negotiations, tiny + high missingness |
| 89 | `vowel` | Classification (11-class) | 990 | Vowel recognition |
| 90 | `waveform-5000` | Classification (3-class) | 5,000 | Synthetic-in-origin but classic real benchmark |
| 91 | `spectf` | Classification (binary) | 349 | Cardiac SPECT images, features only |
| 92 | `spectrometer` | Classification (many classes) | 531 | High-dimensional (102 features) |
| 93 | `solar-flare` | Classification/Regression | 315 | Solar flare frequency prediction |
| 94 | `soybean` | Classification (many classes) | 683 | Plant disease diagnosis, categorical |
| 95 | `splice` | Classification (3-class) | 3,190 | DNA splice-junction sequences |
| 96 | `sick` | Classification (binary) | 3,772 | Thyroid sick/not-sick, imbalanced |
| 97 | `colic` | Classification (binary) | 368 | Horse colic outcome, many missing values |
| 98 | `meta` | Regression | 528 | Meta-learning algorithm performance data |
| 99 | `puma8NH` | Regression | 8,192 | Robot arm dynamics simulation |
| 100 | `puma32H` | Regression | 8,192 | Robot arm, higher-dimensional variant |
| 101 | `bank8FM` | Regression | 8,192 | Bank queue simulation |
| 102 | `bank32nh` | Regression | 8,192 | Bank queue simulation, higher-dimensional |
| 103 | `cpu_act` | Regression | 8,192 | Computer system activity prediction |
| 104 | `cpu_small` | Regression | 8,192 | Smaller-feature variant of cpu_act |
| 105 | `delta_ailerons` | Regression | 7,129 | Aircraft control (ailerons) |
| 106 | `delta_elevators` | Regression | 9,517 | Aircraft control (elevators) |
| 107 | `pollen` | Regression | 3,848 | Synthetic-origin pollen grain measurements |
| 108 | `space_ga` | Regression | 3,107 | US county-level social/political data |
| 109 | `stock` | Regression | 950 | Stock price prediction |
| 110 | `elevators` | Regression | 16,599 | Aircraft elevator control, larger variant |
| 111 | `house_16H` | Regression | 22,784 | House pricing, 16 features |
| 112 | `house_8L` | Regression | 22,784 | House pricing, 8 features |
| 113 | `fried` | Regression | 40,768 | Friedman-style synthetic-origin, large |
| 114 | `2dplanes` | Regression | 40,768 | Synthetic-origin regression benchmark |
| 115 | `mv` | Regression | 40,768 | Mixed-variable synthetic-origin regression |
| 116 | `quake` | Regression | 2,178 | Earthquake magnitude prediction |
| 117 | `socmob` | Regression/Classification | 1,156 | Social mobility count data |
| 118 | `no2` | Regression | 500 | Air pollution (NO2) prediction |
| 119 | `plasma_retinol` | Regression | 315 | Plasma retinol/beta-carotene levels |
| 120 | `visualizing_environmental` | Regression | 111 | Small environmental time-series-like data |
| 121 | `analcatdata_apnea1` | Classification | 475 | Sleep apnea diagnosis, variant 1 |
| 122 | `analcatdata_apnea2` | Classification | 475 | Sleep apnea diagnosis, variant 2 |
| 123 | `analcatdata_apnea3` | Classification | 450 | Sleep apnea diagnosis, variant 3 |
| 124 | `prnn_synth` | Classification (binary) | 250 | Small synthetic-origin, 2D visualizable |
| 125 | `rmftsa_ladata` | Regression | 508 | Time-series-style regression |
| 126 | `sensory` | Regression | 576 | Wine sensory scoring |
| 127 | `SWD` | Classification (ordinal) | 1,000 | Social worker decisions, ordinal target |
| 128 | `triazines` | Regression | 186 | Drug activity regression, high-dimensional (61 features) |
| 129 | `veteran` | Regression | 137 | Veteran's lung cancer survival data |
| 130 | `autoPrice` | Regression | 159 | Car price regression, small |
| 131 | `chscase_geyser1` | Regression | 222 | Old Faithful geyser, regression framing |
| 132 | `disclosure_x_bias` | Regression | 662 | Small statistical disclosure dataset |
| 133 | `arsenic-female-bladder` | Regression | 559 | Arsenic exposure epidemiology data |
| 134 | `chatfield_4` | Regression | 235 | Small time-series-style regression |

---

## 🧪 6. Synthetic Generators — `sklearn.datasets.make_*` (83)

Zero network dependency, fully reproducible with `random_state=`, and parameterized specifically to target each Classical ML topic ahead.

### Regression (7)

| # | Recipe | Load Code | Targets which topic |
|---|---|---|---|
| 135 | Linear, low noise | `make_regression(n_samples=200, n_features=5, noise=10, random_state=42)` | Linear Regression basics |
| 136 | Single feature (visualizable) | `make_regression(n_samples=200, n_features=1, noise=20, random_state=42)` | Simple/Polynomial Regression, plotting the fit line |
| 137 | Multi-output | `make_regression(n_samples=200, n_features=5, n_targets=2, random_state=42)` | Multi-output regression |
| 138 | High noise | `make_regression(n_samples=200, n_features=5, noise=50, random_state=42)` | Ridge/Lasso robustness comparison |
| 139 | Friedman #1 | `make_friedman1(n_samples=200, random_state=42)` | Non-linear regression (tree/boosting) |
| 140 | Friedman #2 | `make_friedman2(n_samples=200, random_state=42)` | Non-linear regression variant |
| 141 | Friedman #3 | `make_friedman3(n_samples=200, random_state=42)` | Non-linear regression variant |

### Classification (10)

| # | Recipe | Load Code | Targets which topic |
|---|---|---|---|
| 142 | Binary, balanced | `make_classification(n_samples=300, n_classes=2, random_state=42)` | Logistic Regression, SVM basics |
| 143 | Imbalanced (90/10) | `make_classification(n_samples=300, weights=[0.9, 0.1], random_state=42)` | Class-imbalance handling |
| 144 | Multiclass (4-class) | `make_classification(n_samples=300, n_classes=4, n_informative=4, random_state=42)` | Multiclass classifiers |
| 145 | 2D visualizable | `make_classification(n_samples=300, n_features=2, n_informative=2, n_redundant=0, random_state=42)` | Decision boundary plotting |
| 146 | Gaussian quantiles | `make_gaussian_quantiles(n_samples=300, random_state=42)` | Non-linear boundary practice |
| 147 | Hastie 10.2 | `make_hastie_10_2(n_samples=300, random_state=42)` | AdaBoost/Boosting benchmark (used in sklearn's own docs) |
| 148 | Moons | `make_moons(n_samples=300, noise=0.1, random_state=42)` | Kernel SVM, KNN non-linear boundaries |
| 149 | Circles | `make_circles(n_samples=300, noise=0.05, random_state=42)` | Kernel trick demonstration |
| 150 | Moons (low noise, for clustering) | `make_moons(n_samples=300, noise=0.05, random_state=42)` | DBSCAN non-convex cluster practice |
| 151 | Circles (for clustering) | `make_circles(n_samples=300, noise=0.03, factor=0.5, random_state=42)` | DBSCAN non-convex cluster practice |

### Clustering (4)

| # | Recipe | Load Code | Targets which topic |
|---|---|---|---|
| 152 | 3 well-separated blobs | `make_blobs(n_samples=300, centers=3, random_state=42)` | K-Means introduction |
| 153 | 5 overlapping blobs | `make_blobs(n_samples=300, centers=5, cluster_std=2.5, random_state=42)` | Gaussian Mixture Models |
| 154 | 2 simple blobs | `make_blobs(n_samples=300, centers=2, n_features=2, random_state=42)` | Simple 2D clustering visualization |
| 155 | Biclusters | `make_biclusters(shape=(100, 50), n_clusters=3, random_state=42)` | Advanced biclustering practice |

### Manifold / Dimensionality Reduction (3)

| # | Recipe | Load Code | Targets which topic |
|---|---|---|---|
| 156 | Swiss roll | `make_swiss_roll(n_samples=300, random_state=42)` | t-SNE/UMAP non-linear manifold demo |
| 157 | S-curve | `make_s_curve(n_samples=300, random_state=42)` | Manifold learning comparison |
| 158 | Low-rank matrix | `make_low_rank_matrix(n_samples=100, n_features=20, random_state=42)` | PCA with controllable effective rank |

### Math / Misc (4)

| # | Recipe | Load Code | Targets which topic |
|---|---|---|---|
| 159 | SPD matrix | `make_spd_matrix(n_dim=5, random_state=42)` | Covariance matrix practice (ties to Math Refresher) |
| 160 | Sparse uncorrelated | `make_sparse_uncorrelated(n_samples=200, random_state=42)` | Feature selection (only a few features matter) |
| 161 | Multilabel classification | `make_multilabel_classification(n_samples=200, n_classes=3, random_state=42)` | Multi-label practice (bonus, beyond this series' scope) |
| 162 | Checkerboard | `make_checkerboard(shape=(100, 50), n_clusters=3, random_state=42)` | Advanced biclustering variant |

---

## 🗺️ Which Dataset for Which Topic?

| Classical ML topic (coming next) | Recommended datasets |
|---|---|
| Linear/Polynomial Regression | #135, #136, #4 (Diabetes), #7 (California Housing) |
| Ridge/Lasso/ElasticNet | #138 (high noise), #160 (sparse/uncorrelated) — or `synthetic/regression_high_noise.csv` |
| Logistic Regression | #142, #37 (Adult), #65 (Diabetes classification) |
| KNN (classification/regression) | #148 (Moons), #1 (Iris), #17 (Penguins) |
| Naive Bayes | #39 (Mushroom), #40 (Spambase) |
| Decision Trees / Random Forest | #46 (Car), #61 (Blood Transfusion), any classification set |
| SVM (kernel trick) | #149 (Circles), #148 (Moons) |
| Boosting (AdaBoost/XGBoost/etc.) | #147 (Hastie 10.2), #59 (Wine Quality) |
| K-Means / Hierarchical / DBSCAN | #152, #153, #150, #151, #31 (Geyser — the classic!) |
| PCA / Dimensionality Reduction | #158, #26 (Brain Networks), #8 (Digits) |
| t-SNE / UMAP | #156 (Swiss Roll), #157 (S-Curve) |
| Association Rules (Apriori) | #46 (Car), #72 (Nursery) — categorical-heavy sets work best |
| Model Evaluation & Tuning | Any dataset above — practice CV/tuning on a few different ones |
| Class-imbalance practice | `synthetic/classification_imbalanced_99_1.csv` (and siblings: 90/10, 95/5, 80/20 variants) |

---

## ⚠️ Caveats & Notes

1. **OpenML names can occasionally have multiple versions.** If `fetch_openml(name=...)` ever raises a version-ambiguity error, add `version=1` (or check [openml.org](https://www.openml.org) to search for the current canonical name/version).
2. **All 162 cataloged entries (and all 212 CSV files) were live-verified while building this catalog** — every name/function call was actually executed successfully and the resulting file inspected. If one ever breaks in the future (OpenML dataset removed/renamed), search openml.org for a replacement.
3. **Large datasets** (Covertype, RCV1, Adult, Diamonds, Letter, and several OpenML sets) were downsampled to 15,000 rows in the CSV export (see `MANIFEST_curated.csv`'s `sampled_from` column) — use the API load call for the full, un-sampled version when you specifically want to practice at scale.
4. **First API download requires internet**; every subsequent load is served from local cache (`~/scikit_learn_data/` for sklearn/OpenML, `~/seaborn-data/` for seaborn). The CSV files in this repo need no network at all, once cloned.
5. **Licensing**: all datasets here are long-established public research/benchmark datasets distributed through official library APIs. If you redistribute a *derived* file from any of them, check the original dataset's license/citation requirements first (most require attribution only).

---
[← Back to Datasets repo overview](README.md) · [Foundation series →](https://github.com/mdnuruzzamanKALLOL/Statistical-Machine-Learning-Foundation)
