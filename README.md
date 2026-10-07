# OCD Patient Records: Exploratory Data Analysis

An exploratory data analysis of 1,500 records examining demographics, symptom duration, obsession and compulsion categories, and recorded symptom scores. Developed by **Anita Aifesehi** as a data analytics capstone project, the notebook demonstrates data inspection, careful handling of categorical values, descriptive analysis, and visualization with Python.

## Overview

The project explores how recorded obsession and compulsion scores vary across selected diagnostic and symptom groups, and whether age and symptom duration show linear relationships with those scores. It brings together record counts, group averages, distributions, and correlations to support clear reporting and identify questions for further investigation.

The analysis is descriptive. Its findings apply to the supplied dataset and do not establish causation, treatment effectiveness, or population-wide patterns.

## Objectives

- Inspect the dataset's structure, data types, apparent missing values, and duplicate rows.
- Preserve meaningful `"None"` responses in diagnosis and medication fields.
- Compare obsession scores by depression diagnosis and obsession type.
- Compare compulsion scores by anxiety diagnosis.
- Examine correlations between age, symptom duration, and recorded symptom scores.
- Check symptom duration for outliers using the interquartile range (IQR) method.
- Communicate patterns through summary tables and visualizations.

## Dataset

**Input file:** `ocd_patient_dataset.csv`  
**Size shown in the notebook:** 1,500 rows and 17 columns  
**Source cited in the notebook:** [OCD Patient Dataset: Demographics & Clinical Data on Kaggle](https://www.kaggle.com/datasets/ohinhaque/ocd-patient-dataset-demographics-and-clinical-data/data)

| Field group | Included columns |
| --- | --- |
| Identifier | Patient ID |
| Demographics | Age, Gender, Ethnicity, Marital Status, Education Level |
| History | OCD Diagnosis Date, Duration of Symptoms (months), Previous Diagnoses, Family History of OCD |
| Symptoms | Obsession Type, Compulsion Type |
| Recorded scores | Y-BOCS Score (Obsessions), Y-BOCS Score (Compulsions) |
| Other diagnoses and medication | Depression Diagnosis, Anxiety Diagnosis, Medications |

### Handling apparent missing values

The initial CSV import interpreted the literal text `"None"` as a missing value in **Previous Diagnoses** (248 records) and **Medications** (386 records). The notebook reloads the file with `keep_default_na=False` to preserve those entries as categories, interpreted as no previous diagnosis and no medication.

Following that reload, the saved checks report zero pandas null values and zero duplicate rows. All 1,500 rows are retained. Because disabling default missing-value parsing also preserves other text and empty strings, a zero null count alone is not a complete validation of missing data. The duplicate-row check also does not establish that Patient IDs are unique.

## Tools and Technologies

| Tool | Purpose |
| --- | --- |
| Python | Programming language; notebook metadata records version 3.12.7 |
| pandas | CSV loading, data inspection, descriptive statistics, grouping, and correlations |
| Matplotlib | Figure layout, labels, and chart rendering |
| Seaborn | Statistical visualizations |
| Jupyter Notebook | Interactive analysis and written interpretation |

## Workflow and Methodology

1. **Load and inspect the data:** review sample rows, column types, dimensions, and summary statistics.
2. **Review data quality:** investigate apparent missing values, preserve valid categorical responses, and check for duplicate rows.
3. **Compare groups:** calculate record counts and mean scores by depression diagnosis, anxiety diagnosis, and obsession type.
4. **Explore numeric relationships:** calculate a Pearson correlation matrix for age, symptom duration, obsession scores, and compulsion scores.
5. **Check outliers:** apply the 1.5 × IQR rule to symptom duration and visualize the distribution with a box plot.
6. **Visualize and interpret:** create an age histogram, obsession-type count chart, diagnosis-based score box plots, a duration–score scatter plot, and a correlation heatmap.
7. **Discuss reporting implications:** summarize descriptive patterns and document questions about data quality and interpretation.

## Key Findings

The following results are supported by the notebook's saved code outputs:

| Analysis | Observed result |
| --- | --- |
| Age | Ages range from 18 to 75 years, with a mean of 46.78 and a median of 47. |
| Symptom duration | Duration ranges from 6 to 240 months, with a median of 121 months. |
| Overall scores | Mean recorded obsession score: 20.05; mean recorded compulsion score: 19.63. |
| Obsession-type frequency | Harm-related is the most common category (333 records); Hoarding is the least common (278). |
| Obsession scores by type | Hoarding has the highest mean (21.01), while Religious has the lowest (19.23). |
| Depression diagnosis | Mean obsession scores are nearly identical: 20.04 with a depression diagnosis and 20.05 without. |
| Anxiety diagnosis | Mean compulsion scores are 19.33 with an anxiety diagnosis and 19.93 without—a difference of approximately 0.60 points. |
| Numeric relationships | Pairwise correlations range from −0.003 to 0.040, indicating very weak linear relationships among the selected measures. |
| Symptom-duration outliers | No observations fall outside the IQR bounds of −107 and 349 months. |

These results illustrate why category frequency and average score should be reported together: the most frequent obsession category is not the category with the highest mean score. Near-zero correlations do not prove that variables are independent or rule out nonlinear relationships.

## Scope and Limitations

- The notebook contains additional narrative claims about statistical significance, compulsion-type comparisons, repeated identifiers, and possible synthetic data. Corresponding calculation cells are not included, so those claims are not presented here as verified findings.
- Both score columns have observed values from 0 to 40. Their definitions and scoring conventions should be confirmed with the dataset provider before clinical interpretation.
- The dataset's provenance and representativeness are not established by the analysis. Patterns should not be generalized to all people with OCD.
- The project does not train a predictive model or evaluate treatment outcomes.
- The findings above reflect saved notebook outputs; reproducing them requires the source CSV.

## Project Structure

The layout below shows the notebook, this README, and the dataset placement expected by the portable setup instructions. The CSV must be obtained separately if it is not already included in your checkout.

```text
.
├── README.md
├── Capstone_Project.ipynb
└── ocd_patient_dataset.csv    # Required input; obtain from the cited source
```

## How to Run

### 1. Prepare the project files

Download or clone the repository and open the folder containing `Capstone_Project.ipynb`. Obtain `ocd_patient_dataset.csv` from the cited dataset source and place it beside the notebook.

### 2. Install the dependencies

Use Python 3.12 to closely match the notebook's recorded environment. From a terminal in the project folder, run:

```bash
python -m pip install pandas matplotlib seaborn notebook
```

Exact package versions are not recorded in the notebook, so this installs the currently available versions rather than recreating a pinned environment.

### 3. Update both dataset paths

The notebook contains **two** `pd.read_csv(...)` calls pointing to an absolute Windows path on the author's computer. Replace the path in each call with the local filename.

For the initial import:

```python
df = pd.read_csv("ocd_patient_dataset.csv")
```

For the subsequent reload that preserves `"None"` categories:

```python
df = pd.read_csv("ocd_patient_dataset.csv", keep_default_na=False)
```

Keep both steps to reproduce the notebook's demonstration of default missing-value parsing and its correction.

### 4. Open and execute the notebook

```bash
python -m notebook
```

Open `Capstone_Project.ipynb`, select a Python kernel with the dependencies installed, and run all cells from top to bottom. If the saved `conda-base-py` kernel is unavailable, choose your installed Python kernel.

The notebook displays summary tables and charts inline; its code does not export a separate report or cleaned dataset.

## Author

**Anita Aifesehi**  
Data Analytics Capstone Project

This project demonstrates practical skills in data inspection, categorical-value handling, exploratory analysis, visualization, and communicating analytical findings.
