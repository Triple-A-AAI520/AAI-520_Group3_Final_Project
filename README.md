ReadME.md EXAMPLE

# Mental Health Data Processing & Analysis

This repository contains the code, notebooks, and documentation for ingesting, cleaning, and exploring a collection of Mental Health datasets. It is part of the AAI-500 coursework at the University of San Diego (USD) and brings together multiple contributors’ work on data cleaning, formatting, and initial exploratory analysis.

---

## Project Status

**Active**
The repository is actively maintained. Unused or redundant files have been removed; the main Jupyter notebook incorporates the latest formatting and cleaning steps.

---

## Overview

Over the first weeks of the semester, we collected seven CSV files containing various indicators of mental health prevalence and outcomes (e.g., burden of disease, treatment gaps, depression rates). Our goals are:

1. **Import & Consolidate**

   * Load all Mental Health CSVs (hosted on GitHub) into Google Colab or Jupyter.
   * Keep filenames and DataFrame objects in sync so that each dataset is clearly labeled.

2. **Data Cleaning & Formatting**

   * Rename columns for consistency.
   * Handle missing values (NaNs) using appropriate imputation or removal.
   * Detect and treat outliers via IQR and Z-score methods.
   * Standardize data types and drop any unused columns.

3. **Exploratory Analysis**

   * Generate summary statistics (mean, median, ranges) for each dataset.
   * Create visualizations (histograms, KDEs, boxplots) to inspect distributions and outliers.
   * Track the presence of specific “disorders” or indicators across datasets.

4. **Modular Notebook Structure**

   * **Data Cleaning Notebook** (`formatting.ipynb`)
     Contains step-by-step code to rename columns, fill/drop NaNs, and flag outliers for Datasets 5–7.
   * **Main Analysis Notebook** (`mental_health_analysis.ipynb`)
     Combines all seven datasets into a single workflow: imports, cleaning calls, visualizations, and basic summary tables.

5. **Reproducibility**

   * All raw CSVs are fetched directly from GitHub via API calls.
   * A helper function (`load_csvs_from_github_dir`) ensures that filenames match DataFrame order.
   * Anyone can clone this repo, install dependencies, and run notebooks top-to-bottom to reproduce our cleaning pipeline and initial plots.

---

## Folder Structure

```
.
├── LICENSE
├── README.md
├── formatting.ipynb
├── mental_health_analysis.ipynb
├── requirements.txt
└── utils
    └── load_data.py
```

* **`formatting.ipynb`**
  Contains the standalone data-cleaning pipeline for Datasets 5–7 (column renaming, NaN handling, outlier detection).

* **`mental_health_analysis.ipynb`**
  The primary notebook that:

  1. Imports all seven Mental Health CSVs.
  2. Calls the cleaning functions (or cells) in sequence.
  3. Produces summary tables and visualizations for each dataset.
  4. Demonstrates how to merge cleaned data or compare key indicators.

* **`utils/load_data.py`**
  A small Python module providing `load_csvs_from_github_dir(api_directory_url)`, which fetches every `.csv` in a given GitHub directory and returns a `{ filename: DataFrame }` mapping.

* **`requirements.txt`**
  Lists all necessary Python packages (versions pinned) to run the notebooks end-to-end.

---

## Installation

1. **Clone this repository**

   ```bash
   git clone https://github.com/AAI500TeamProject/thementalists-project.git
   cd thementalists-project
   ```

2. **Create a virtual environment (optional but recommended)**

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

   While the notebooks also import:

   * `pandas`
   * `numpy`
   * `scipy`
   * `seaborn`
   * `matplotlib`
   * `scikit-learn`
   * `requests`

   these are already specified in `requirements.txt`.

4. **Open the Notebooks**
   Launch Jupyter Lab/Notebook or Google Colab:

   * **Local Jupyter**

     ```bash
     jupyter lab
     ```

     Then open `mental_health_analysis.ipynb` (or `formatting.ipynb`).

   * **Google Colab**

     1. Upload `mental_health_analysis.ipynb` to Colab.
     2. Ensure you have Internet access so that the helper function can fetch CSVs from GitHub.

---

## Usage

### 1. Loading All CSVs from GitHub

In your notebook (e.g., at the top of `mental_health_analysis.ipynb`), you’ll see:

```python
from utils.load_data import load_csvs_from_github_dir

# The GitHub API endpoint pointing to the “MentalHealth” directory:
api_url = (
    "https://api.github.com/repos/"
    "AAI500TeamProject/thementalists-project/"
    "contents/Dataset/MentalHealth"
)

# Returns a dict: { filename_1: df_1, filename_2: df_2, … }
dataframes = load_csvs_from_github_dir(api_url)

# If you want a parallel list of names and DataFrames:
file_names = list(dataframes.keys())
dfs_list   = list(dataframes.values())
```

After this cell runs, you have all seven CSVs loaded into Pandas DataFrames in the same order as `file_names`.

### 2. Cleaning / Formatting (in `formatting.ipynb`)

* **Column Renaming**
  We standardize column names (lowercase, underscores instead of spaces, remove special characters). For example:

  ```python
  df.rename(columns=lambda c: c.strip().lower().replace(" ", "_"), inplace=True)
  ```
* **Missing-Value Handling**

  * Identify columns with NaN.
  * For numeric columns, if missingness < 5%, drop those rows; else, consider median imputation.
* **Outlier Detection**

  * We show both **IQR method** (1.5× IQR rule) and **Z-score method** to flag outliers.
  * Visualize with `seaborn.kdeplot` and `boxplot`.
  * Users can choose to drop or winsorize based on domain knowledge.

### 3. Exploratory Analysis (in `mental_health_analysis.ipynb`)

* Each dataset is summarized:

  ```python
  for name, df in dataframes.items():
      print(f"Dataset: {name}")
      display(df.describe())
      sns.histplot(df["some_numeric_column"], kde=True)
      plt.title(f"{name} - Distribution of some_numeric_column")
      plt.show()
  ```
* We compare prevalence rates or treatment gaps across multiple CSVs (where column names are aligned).

---

## Contributors

* **Dylan SD** (*[dylansd@gmail.com](mailto:dylansd@gmail.com)*)

  * Merged latest formatting into main notebook; removed unused notebooks.
* **Mandeep Saini** (*[mandeep.saini@brightcircledatascience.com](mailto:mandeep.saini@brightcircledatascience.com)*)

  * Created and refined `formatting.ipynb`: column renaming, NaN handling (Datasets 5–7).
  * Added cleaned‐data processing for Datasets 5–7.
* **David Scott Dawkins** (*[dscottdawkins@sandiego.edu](mailto:dscottdawkins@sandiego.edu)*)

  * Modularized Week 1 merge: dataset renaming, removed legacy CSVs, split notebook cells, added “disorders” tagging.
* **Quang Tran** (*[qtran@sandiego.edu](mailto:qtran@sandiego.edu)*)

  * Implemented missing value and outlier handling via IQR and Z-score; visualized with KDE for threshold decisions.
* **Andrew Tran** (*[qtran@sandiego.edu](mailto:qtran@sandiego.edu)*)

  * Added new Mental Health Dataset files; initial ingestion.
* **Paul Parks** (*[paul.anthony.parks@gmail.com](mailto:paul.anthony.parks@gmail.com)*) and **Alden Caterio** (*[aldencaterio@gmail.com](mailto:aldencaterio@gmail.com)*)

  * Original setup, initial README and notebook scaffolding (2023 Wine project).

---

## Technologies & Methods

* **Languages & Libraries**

  * Python 3.x
  * pandas, numpy, scipy, scikit-learn
  * seaborn, matplotlib
  * requests (for GitHub API calls)

* **Statistical Methods**

  * Outlier detection (IQR & Z-score)
  * Missing data analysis (drop vs. impute)
  * Basic descriptive statistics (mean, median, quartiles)

* **Environment**

  * Google Colab (tested)
  * Jupyter Notebook / Jupyter Lab (locally tested)

---

## How to Extend

1. **Add More Datasets**

   * If you push additional `.csv` files under `Dataset/MentalHealth`, simply rerun:

     ```python
     dataframes = load_csvs_from_github_dir(api_url)
     ```

     They will automatically appear in `dataframes`.

2. **Customize Cleaning Rules**

   * In `formatting.ipynb`, locate the cells under “Missing-Value Handling” and “Outlier Detection.” Tweak thresholds (e.g., IQR factor, z‐score cutoff) as needed.

3. **Merge & Compare Across Years**

   * Several CSVs contain time series (year, region, prevalence). You can join them on common keys (e.g., `country`, `year`) for cross‐dataset analysis.

4. **Additional Visualizations**

   * Feel free to add more plots (heatmaps, scatterplots, bar charts) in `mental_health_analysis.ipynb` to highlight trends or correlations.

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

## Acknowledgments

* **USD AAI-500 Course** (Professor Leon Shpaner)
* **Dataset Contributors** (World Health Organization (WHO), Institute for Health Metrics and Evaluation (IHME), etc.)
* **Team Members** (listed above) for their ongoing collaboration and code reviews.

---

> *Last updated: June 4, 2025*

