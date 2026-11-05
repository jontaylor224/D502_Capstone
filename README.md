# A Comparison of Reported Pertussis Incidence in U.S. Jurisdictions Before and After the COVID-19 Pandemic

## Project Overview

This project examines whether reported pertussis incidence differed significantly between the pre-pandemic period (2016–2019) and the post-acute-pandemic period (2022–2023) across the 50 U.S. states and the District of Columbia.

The analysis uses annual pertussis surveillance data from the Centers for Disease Control and Prevention (CDC) National Notifiable Diseases Surveillance System (NNDSS), obtained through CDC WONDER.

**Research question:**

> Did reported pertussis incidence differ significantly between the pre-pandemic period (2016–2019) and the post-acute-pandemic period (2022–2023) across the 50 U.S. states and the District of Columbia?

This is a quantitative, retrospective observational analysis. It compares reported surveillance incidence across jurisdictions and does not attempt to estimate all pertussis infections or establish that the COVID-19 pandemic caused changes in reported incidence.

## Repository Contents

All project files are located in the repository's root directory, except for the visualization images.

| File or directory | Description |
|---|---|
| `analysis.ipynb` | Completed Jupyter Notebook containing the data-loading, cleaning, validation, statistical analysis, and visualization code, including saved outputs. |
| `NNDSS_Annual_Summary_Data_2016-2023_Pertussis.csv` | Original CDC NNDSS annual pertussis dataset downloaded from CDC WONDER. |
| `cleaned_pertussis_data.csv` | Prepared dataset containing 408 observations representing 51 jurisdictions across eight years. |
| `analysis.html` | HTML export of the Jupyter Notebook for viewing the analysis without opening Jupyter. |
| `images/` | Directory containing exported data visualizations. |
| `README.md` | Project overview, data documentation, methodology, findings, and reproduction instructions. |

## Data Source

The data were obtained from the CDC National Notifiable Diseases Surveillance System (NNDSS) annual summary data through CDC WONDER:

- **Source:** [CDC WONDER – NNDSS Annual Summary Data](https://wonder.cdc.gov/nndss-annual-summary.html)
- **Years analyzed:** 2016–2023
- **Geographic coverage:** 50 U.S. states and the District of Columbia
- **Subject:** Annual reported pertussis cases and incidence rates

The analysis uses jurisdiction-level surveillance data. The years 2020 and 2021 are retained in the prepared dataset for context but excluded from the comparison of the two study periods.

## Data Preparation

The original CDC data required several preparation steps before analysis:

1. Removed documentation and non-data rows from the downloaded file.
2. Retained the 50 states and the District of Columbia, excluding national aggregate and non-U.S. reporting areas.
3. Combined New York City and New York State excluding New York City into a single New York jurisdiction by summing case counts and population denominators, then recalculating the incidence rate.
4. Addressed six missing published incidence rates. Each missing rate corresponded to zero reported cases and a positive population denominator, so these rates were assigned a value of zero.
5. Validated that the prepared dataset contained 51 jurisdictions for each of the eight years, with no duplicate jurisdiction-year combinations and no missing incidence rates.

The resulting prepared dataset contains **408 rows (51 jurisdictions × 8 years) and 9 columns**.

## Analysis Methodology

The analysis compares two periods:

- **Pre-pandemic:** 2016–2019
- **Post-acute-pandemic:** 2022–2023

The years 2020 and 2021 were excluded from the period comparison.

For each jurisdiction, the mean annual incidence rate was calculated for each period. The two period means were then compared using paired statistical methods, with each jurisdiction serving as its own comparison.

The analysis includes:

- Descriptive statistics comparing the two periods.
- A paired-samples t-test to evaluate the mean difference between periods.
- A 95% confidence interval for the mean paired difference.
- Cohen's *d*_z to estimate effect size.
- A Wilcoxon signed-rank test as a supplementary nonparametric comparison.
- An exact sign test as an additional assessment of the direction of change.
- Visualizations of the jurisdiction-level incidence patterns and changes.

## Reproducing the Analysis

### Prerequisites

The following software and Python libraries are required:

- Python 3
- Jupyter Notebook
- pandas
- NumPy
- SciPy
- Matplotlib

### 1. Clone the repository

Open a terminal and run:

```bash
git clone https://github.com/jontaylor224/D502_Capstone.git
```

Change to the repository directory:

```bash
cd D502_Capstone
```

**Important:** Run the following commands from the repository's root directory. The notebook uses relative file paths to locate the original CDC dataset and save the cleaned dataset.

### 2. Create and activate a virtual environment

Creating a virtual environment keeps the project's Python dependencies isolated.

**Windows PowerShell:**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**Windows Command Prompt:**

```cmd
python -m venv .venv
.venv\Scripts\activate.bat
```

**Linux or macOS:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install the required packages

With the virtual environment activated, run:

```bash
python -m pip install --upgrade pip
python -m pip install jupyter pandas numpy scipy matplotlib
```

### 4. Launch Jupyter Notebook

From the repository's root directory, run:

```bash
jupyter notebook
```

Open `analysis.ipynb` in the Jupyter interface.

Alternatively, JupyterLab can be installed and launched using:

```bash
python -m pip install jupyterlab
jupyter lab
```

### 5. Execute the notebook

Run the notebook cells in sequential order, starting with the first cell.

The notebook performs the following operations:

1. Loads and inspects the original CDC dataset.
2. Removes documentation rows and prepares the jurisdiction-level records.
3. Combines the New York City and New York State excluding New York City reporting areas.
4. Handles missing incidence rates associated with zero reported cases.
5. Validates the prepared dataset and saves it as `cleaned_pertussis_data.csv`.
6. Calculates jurisdiction-level mean incidence rates for the pre-pandemic and post-acute-pandemic periods.
7. Performs descriptive and inferential statistical analyses.
8. Generates visualizations of the results.

### 6. Verify the results

After executing all notebook cells, verify that the following results are produced:

- Prepared dataset shape: 408 rows and 9 columns.
- Number of jurisdictions compared: 51.
- Pre-pandemic mean incidence rate: 6.680 per 100,000.
- Post-acute-pandemic mean incidence rate: 1.457 per 100,000.
- Mean paired difference: −5.223 per 100,000.
- Paired t-test: t(50) = −8.141.
- Paired t-test p-value: 1.00738 × 10⁻¹⁰.
- Cohen's d_z: −1.140.

The notebook also performs the Wilcoxon signed-rank test and exact sign test and generates the supporting visualizations.

The execution of the notebook will create or overwrite `cleaned_pertussis_data.csv` in the repository's root directory.

**Important:** The notebook's data-loading paths must point to the locations of the data files within the cloned repository. If the files are moved or renamed, update the corresponding paths before running the notebook.

## Key Findings

The analysis produced the following results:

| Measure | Result |
|---|---:|
| Pre-pandemic mean incidence rate | 6.680 per 100,000 |
| Post-acute-pandemic mean incidence rate | 1.457 per 100,000 |
| Mean paired difference | −5.223 per 100,000 |
| Relative decrease in the unweighted mean | 78.2% |
| Jurisdictions with a decrease | 50 |
| Jurisdictions with an increase | 1 |
| Paired t-test | *t*(50) = −8.141 |
| Paired t-test p-value | 1.00738 × 10⁻¹⁰ |
| 95% confidence interval | [−6.512, −3.935] |
| Cohen's *d*<sub>z</sub> | −1.140 |
| Wilcoxon signed-rank test p-value | 5.46152 × 10⁻¹⁰ |
| Exact sign test p-value | 4.61853 × 10⁻¹⁴ |

The results indicate a statistically significant difference in reported pertussis incidence between the two study periods. The unweighted mean of jurisdiction-level incidence rates was lower in the post-acute-pandemic period.

The 78.2% decrease describes the change in the unweighted mean of jurisdiction-level rates; it is not a population-weighted national incidence estimate.

## Limitations

Several limitations should be considered when interpreting the findings:

- The analysis uses reported surveillance cases, which may not represent all pertussis infections.
- The CDC pertussis case definition changed effective January 1, 2020, which limits direct comparability across the study periods.
- The years 2020 and 2021 were excluded from the period comparison.
- The analysis uses jurisdiction-level averages and does not weight each jurisdiction by population.
- The statistical findings establish an association between study period and reported incidence differences, not a causal relationship with the COVID-19 pandemic.
- The Shapiro-Wilk test indicated that the paired differences departed from normality. The Wilcoxon signed-rank test was therefore included as a supplementary nonparametric analysis; its symmetry assumption was not formally evaluated.

## References

Centers for Disease Control and Prevention. (n.d.). *National Notifiable Diseases Surveillance System (NNDSS): Annual summary data, 2016–2023*. CDC WONDER. https://wonder.cdc.gov/nndss-annual-summary.html

Rubis, A. B., Cole, M., Tondella, M. L., Pawloski, L. C., Youngkin, E., Firmender, P., Aden, V., Cruz, V., Stanislawski, E., Wester, R., Cieslak, P. R., Acosta, A. M., & Skoff, T. H. (2024). Assessing the impact of the 2020 Council of State and Territorial Epidemiologists case definition for pertussis on reported pertussis cases. *Clinical Infectious Diseases, 78*(6), 1727–1731. https://doi.org/10.1093/cid/ciae207

Chapman, P., Clinton, J., Kerber, R., Khabaza, T., Reinartz, T., Shearer, C., & Wirth, R. (2000). *CRISP-DM 1.0: Step-by-step data mining guide*. SPSS Inc.

---

## Project Deliverable

This repository is provided as supporting evidence for the WGU D502 Data Analytics Capstone project. It contains the source data, prepared analysis data, code, and documentation needed to inspect and reproduce the analysis.
