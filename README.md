# A Comparison of Reported Pertussis Incidence in U.S. Jurisdictions Before and After the COVID-19 Pandemic

## Project Overview

This project examines whether reported pertussis incidence differed significantly between the pre-pandemic period (2016–2019) and the post-acute-pandemic period (2022–2023) across the 50 U.S. states and the District of Columbia.

The analysis uses annual pertussis surveillance data from the Centers for Disease Control and Prevention (CDC) National Notifiable Diseases Surveillance System (NNDSS), obtained through CDC WONDER.

**Research question:**

> Did reported pertussis incidence differ significantly between the pre-pandemic period (2016–2019) and the post-acute-pandemic period (2022–2023) across the 50 U.S. states and the District of Columbia?

This is a quantitative, retrospective observational analysis. It compares reported surveillance incidence across jurisdictions and does not attempt to estimate all pertussis infections or establish that the COVID-19 pandemic caused changes in reported incidence.

## Repository Contents

The repository contains the materials needed to inspect and reproduce the analysis.

| File or directory | Description |
|---|---|
| `analysis.ipynb` | Jupyter Notebook containing the data-loading, cleaning, validation, statistical analysis, and visualization code. |
| `NNDSS_Annual_Summary_Data_2016-2023_Pertussis.csv` | Original CDC dataset |
| `cleaned_pertussis_data.csv` | Cleaned dataset for analysis |
| `/images` | Directory of data visualization images for export if needed |

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

- Python 3
- Jupyter Notebook or JupyterLab
- The project repository cloned or downloaded to your computer
- The original CDC data file and prepared analysis data, as included in the repository

### 1. Clone the repository

Open a terminal and run:

```bash
git clone https://github.com/jontaylor224/D502_Capstone
```

Change to the repository directory:

```bash
cd [REPOSITORY-DIRECTORY]
```

### 2. Create and activate a virtual environment

Creating a separate environment helps keep the project's Python dependencies isolated.

**Windows:**

```bash
python -m venv .venv
.venv\Scripts\activate
```

**Linux or macOS:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

Install the dependencies used by the notebook. At a minimum, the analysis uses the following Python packages:

```bash
python -m pip install jupyter pandas numpy scipy matplotlib
```

If additional packages are imported by the notebook, install those as well.

### 4. Open the Jupyter Notebook

From the repository directory, run:

```bash
jupyter notebook
```

Open `analysis(7).ipynb` in the Jupyter interface.

### 5. Run the analysis

Execute the notebook cells in order, starting with the first cell.

The notebook performs the following operations:

1. Loads and inspects the source data.
2. Cleans and prepares the jurisdiction-level dataset.
3. Combines the New York reporting areas.
4. Handles missing incidence rates associated with zero reported cases.
5. Validates and exports the prepared dataset.
6. Calculates and compares incidence rates for the two study periods.
7. Performs statistical tests and generates visualizations.

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
