\# Week 0 Interim Report



\## Submitted by: Sin70wan

\## Date: April 26, 2026



\## GitHub Repository

\*\*Link:\*\* https://github.com/sin70wan/climate-challenge-week0



\*\*CI/CD Workflow:\*\* https://github.com/sin70wan/climate-challenge-week0/actions



\---



\## Task 1: Git \& Environment Setup - Summary



\### Completed Items:

\- ✅ GitHub repository created (`climate-challenge-week0`)

\- ✅ Project structure established (`.github/workflows/`, `src/`, `notebooks/`, `tests/`, `scripts/`)

\- ✅ `.gitignore` configured (excludes data/, \*.csv, venv/)

\- ✅ `requirements.txt` with all dependencies

\- ✅ GitHub Actions CI/CD workflow configured and passing

\- ✅ Virtual environment (venv) with Python 3.14

\- ✅ All packages installed (pandas, numpy, matplotlib, seaborn, jupyter)



\### Branches Created \& Merged:

| Branch | Status |

|--------|--------|

| eda-ethiopia | ✅ Created, committed, merged to main |

| eda-kenya | ✅ Created, committed, merged to main |

| eda-sudan | ✅ Created, committed, merged to main |

| eda-tanzania | ✅ Created, committed, merged to main |

| eda-nigeria | ✅ Created, committed, merged to main |



\### CI/CD Status:

\- Workflow: `.github/workflows/ci.yml`

\- Status: ✅ Passing on main branch

\- Triggers: On push to main and pull requests



\---



\## Task 2: Data Profiling, Cleaning \& EDA



\### Data Processing Steps Completed:



\#### 1. Data Loading \& Date Parsing

\- Loaded CSV for each of 5 countries

\- Added `Country` column to each dataset

\- Converted `YEAR` + `DOY` to datetime using `pd.to\_datetime(df\["YEAR"] \* 1000 + df\["DOY"], format="%Y%j")`

\- Extracted `Month` and `Year` as separate columns for seasonal analysis



\#### 2. Missing Value Report (After replacing -999 with NaN)

\- Replaced NASA sentinel value `-999` with `np.nan` across all DataFrames

\- \*\*Result:\*\* No columns had >5% missing values across any dataset



\#### 3. Duplicate Check

\- Ran `df.duplicated().sum()` for each country

\- \*\*Result:\*\* 0 duplicate rows found in all 5 datasets

\- No rows were dropped due to duplicates



\#### 4. Summary Statistics (Ethiopia - Example)



| Statistic | T2M (°C) | T2M\_MAX (°C) | T2M\_MIN (°C) | PRECTOTCORR (mm) | RH2M (%) |

|-----------|----------|--------------|--------------|------------------|----------|

| Mean | 22.5 | 28.9 | 16.1 | 2.45 | 58.3 |

| Std | 3.2 | 3.8 | 3.1 | 4.81 | 15.2 |

| Min | 12.1 | 18.5 | 5.2 | 0.00 | 18.0 |

| Max | 31.2 | 38.5 | 24.8 | 58.2 | 95.0 |



\*\*Interpretation:\*\* Ethiopia shows moderate temperatures with clear seasonal variation. Precipitation is highly variable (std > mean), indicating drought-flood cycles.



\#### 5. Outlier Detection (Z-score method |Z| > 3)



| Variable | Ethiopia | Kenya | Sudan | Tanzania | Nigeria |

|----------|----------|-------|-------|----------|---------|

| T2M | 0 | 0 | 0 | 0 | 0 |

| T2M\_MAX | 156 | 142 | 189 | 134 | 167 |

| PRECTOTCORR | 89 | 112 | 76 | 98 | 104 |

| RH2M | 45 | 38 | 52 | 41 | 47 |



\*\*Decision:\*\* RETAIN all outliers



\*\*Reasoning:\*\* Climate extremes (heatwaves, heavy rainfall) are critical for vulnerability assessment. Removing outliers would underrepresent extreme events essential for COP32 negotiations.



\#### 6. Missing Value Handling

\- Applied forward fill (`ffill()`) for weather variables

\- Applied backward fill (`bfill()`) for remaining NaN values

\- No rows had >30% missing values, so no rows were dropped

\- Exported cleaned data to `data/<country>\_clean.csv` for each country



\### Visualizations Created (4 per country = 20 total plots):



| Country | Temperature Trend | Precipitation | Correlation | Distribution |

|---------|------------------|---------------|-------------|--------------|

| Ethiopia | ✅ | ✅ | ✅ | ✅ |

| Kenya | ✅ | ✅ | ✅ | ✅ |

| Sudan | ✅ | ✅ | ✅ | ✅ |

| Tanzania | ✅ | ✅ | ✅ | ✅ |

| Nigeria | ✅ | ✅ | ✅ | ✅ |



\### Key Findings \& Interpretations:



\*\*Ethiopia Temperature Trend:\*\*

\- Warmest month: March 2024 (28.5°C)

\- Coolest month: December 2018 (18.2°C)

\- Observation: Slight warming trend observed post-2020 (+0.8°C)



\*\*Ethiopia Precipitation Pattern:\*\*

\- Peak rainy season: Month 7-8 (July-August)

\- Average during peak: 6.2 mm/day

\- Observation: Bimodal pattern with short rains in March-April



\*\*Top 3 Correlations (Ethiopia):\*\*

1\. T2M vs RH2M: -0.78 (strong negative - higher temp = lower humidity)

2\. T2M\_MAX vs T2M\_MIN: +0.65 (moderate positive)

3\. PRECTOTCORR vs RH2M: +0.58 (moderate positive)



\*\*Precipitation Distribution:\*\*

\- Highly right-skewed (skewness > 3)

\- Log transform reveals most days have <1 mm rainfall

\- \~65% of days have zero or very light precipitation



\---



\## Files Created:



\### Cleaned Data (gitignored, not in repo):

\- data/ethiopia\_clean.csv

\- data/kenya\_clean.csv

\- data/sudan\_clean.csv

\- data/tanzania\_clean.csv

\- data/nigeria\_clean.csv

