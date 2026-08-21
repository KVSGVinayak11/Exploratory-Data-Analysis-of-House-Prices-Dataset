# Exploratory Data Analysis — House Prices

An end-to-end EDA and data preprocessing notebook built on a **House Prices** dataset. The project covers missing-value imputation with before/after distribution comparisons, categorical encoding, numerical normalization, discretization, outlier handling, and a correlation-based feature selection step against the target variable `SalePrice`.

## 📊 Dataset

- **Source:** `house prices.csv`
- **Target variable:** `SalePrice`
- **Key fields used throughout the analysis:**
  - Numerical with missing values: `LotFrontage`, `MasVnrArea`, `GarageYrBlt`
  - Categorical: `LotShape`, `LotConfig`, `Foundation`, `BsmtExposure`, `HeatingQC`, `GarageType`

> Place `house prices.csv` in the working directory (or update the file path in the first cell) before running the notebook.

## 📁 Repository Structure

```
.
├── Exploratory_Data_Analysis_-_Houseprices.ipynb   # Main notebook
├── house prices.csv                                # Dataset (not included — add your own)
└── README.md
```

## 🔍 What's Inside

The notebook is organized into clear, self-contained sections:

### 1. Data Reading
- Load the dataset with `pandas` and inspect summary statistics (`df.describe()`).

### 2. Missing Value Handling
Missing-value percentages are computed per column, and multiple imputation strategies are applied to `LotFrontage`, `MasVnrArea`, and `GarageYrBlt` — **each followed by a before/after distribution comparison using histograms**:
- **Mean Imputation**
- **Median Imputation**
- **Mode Imputation**
- **Frequency (Mode) Imputation for Categorical Data** — applied to `BsmtExposure` and `GarageType`

### 3. Encoding Categorical Data
Applied to `LotShape`, `LotConfig`, `Foundation`, `BsmtExposure`, `HeatingQC`, `GarageType`, each visualized with KDE plots:
- **Label Encoding** (`sklearn.LabelEncoder`)
- **Label Encoding after Frequency/Mode Imputation** — compares encoded distributions before vs. after imputation
- **Frequency Encoding** (value-count based mapping)
- **Ordinal Encoding** (ordered by mean `SalePrice` per category)
- **Mean (Target) Encoding** (category mean of `SalePrice`)

### 4. Normalization for Numerical Data
Applied to `LotFrontage`, `MasVnrArea`, `GarageYrBlt`, each with before/after distribution plots:
- **Min-Max Normalization**
- **Z-Score Normalization** (`StandardScaler`)
- **Decimal Scaling Normalization**

### 5. Discretisation
- **Equal-Width Discretisation** (on normalized `LotFrontage` and `GarageYrBlt`)
- **Equal-Frequency Discretisation** (`pd.qcut`, on normalized `LotFrontage`)
- **K-Means Discretisation** (`KBinsDiscretizer`, `strategy='kmeans'`)
- **Decision Tree Discretisation** (probability-based binning using `DecisionTreeClassifier` against `SalePrice`)

### 6. Outlier Handling
Boxplot-based inspection followed by two treatment strategies on normalized `LotFrontage` and `GarageYrBlt`:
- **Outlier Trimming** — IQR-based removal of out-of-range rows
- **Outlier Capping** — clipping values to the 5th/95th percentile

### 7. Feature Correlation & Selection
- Assembles a `final_df` combining label-encoded categorical features with cleaned numerical features.
- Generates a **correlation heatmap** (`seaborn.heatmap`) against `SalePrice`.
- Identifies the most correlated attributes with `SalePrice`: `le_Foundation`, `GarageYrBlt`, `MasVnrArea`, and `LotFrontage`.

## 🛠️ Tech Stack

| Library | Purpose |
|---|---|
| `pandas` | Data manipulation |
| `numpy` | Numerical operations |
| `matplotlib` / `seaborn` | Visualization (histograms, KDE plots, boxplots, heatmaps) |
| `scikit-learn` | Encoding, scaling, discretization, tree-based binning |

## 🚀 Getting Started

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

### Run the notebook
```bash
git clone <your-repo-url>
cd <your-repo-folder>
jupyter notebook "Exploratory_Data_Analysis_-_Houseprices.ipynb"
```

Update the CSV path in the first code cell to point to your local copy of `house prices.csv`, then run all cells sequentially.

## 📈 Key Takeaways

- Every imputation, encoding, and normalization technique is validated visually (histogram/KDE before vs. after) rather than applied blindly.
- Demonstrates a full categorical-encoding toolkit and when each technique (label, frequency, ordinal, target/mean) is appropriate.
- Includes an outlier-handling comparison (trimming vs. capping) not commonly covered alongside encoding/normalization workflows.
- Concludes with a correlation heatmap to identify which engineered features are most predictive of `SalePrice` — a natural bridge into feature selection / model building.

## 🤝 Contributing

Feel free to open issues or submit pull requests with improvements, additional techniques, or bug fixes.

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).
