# Healthcare Operations & Patient Risk Analytics

## Project overview

A data analytics capstone examining Emergency Department (ED) provider waiting times and Intensive Care Unit (ICU) sepsis outcomes. The project uses Python for cleaning, exploratory analysis, and baseline modeling, with Power BI for management dashboards.

**Purpose:** Identify patterns associated with ED waiting times; compare ICU sepsis outcome groups; assess baseline regression/classification model performance; communicate defensible operational recommendations.

## Datasets

- `ED_Waiting_Time_Data.xlsx` — 6,000 ED visit records.  
- `ICU_Sepsis_Patient_Summary.xlsx` — 180 ICU patient records including outcome and onset fields.  
- `ICU_Sepsis_Patient_Data.xlsx` — accompanying *synthetic educational* clinical data.  
- `ICU_Sepsis_Patient_Data_Dictionary.xlsx` — clinical data definitions.

Keep original files in `data/raw/`. The original instructor files may have been distributed as CSV; this project uses Excel copies. Do **not** commit instructor-provided files to a public repository without permission.

## Repository structure

```
healthcare-analytics-capstone/
├── data/
│   ├── raw/               # source datasets (not tracked by default)
│   └── processed/         # regenerated CSV outputs (not tracked by default)
├── notebooks/
│   ├── 01_ED_Analysis.ipynb
│   └── 02_ICU_Sepsis_Analysis.ipynb
├── dashboard/             # Power BI .pbix and optional exported PDF
├── reports/               # 8–12 page executive report
├── images/                # exported figures and confusion matrices
├── README.md
├── requirements.txt
└── .gitignore
```

## Approach

### ED

- Audit missing values, data types, duplicates, and unusual values.  
- Explore waiting-time distributions by department, triage, arrival hour, day type and season.  
- Examine queue size and staffing associations.  
- Compare Linear Regression, Decision Tree Regression, and Random Forest Regression using MAE, RMSE, and R².

### ICU

- Join summary and synthetic clinical data by `patient_id`, with one-to-one validation.  
- Summarize age, gender, length of stay, sepsis outcomes, and onset timing.  
- Compare Logistic Regression, Decision Tree, and Random Forest classification using accuracy, precision, recall, F1 and ROC-AUC, plus confusion matrices.  
- Exclude outcome-derived information from admission-time predictions.

## Selected findings

- **ED:** 6,000 visits; average wait **42.04 minutes**, median **42.60 minutes**, and 90th percentile **71.70 minutes**.  
- **ED:** Weekend average waiting time was **53.00 minutes**, versus **37.89 minutes** on weekdays. Greater queue size generally corresponded to longer waits, while higher staffing generally corresponded to shorter waits; these are associations, not proven causal effects.  
- **ICU:** **50 of 180 patients (27.8%)** developed sepsis. The average ages of sepsis and non-sepsis groups were similar, while mean ICU length of stay was **43.34 versus 39.05 hours**.  
- **Classification:** In the test set shown in the project confusion matrices, the three baseline models identified few actual sepsis cases; recall was **0% (Logistic Regression)** and **10% (Decision Tree and Random Forest)**. These models are **not suitable for clinical use**.

## How to reproduce

1. Install Python and the packages from `requirements.txt`, or open the notebooks in Google Colab.  
2. Obtain the original datasets through the course/instructor and place them in `data/raw/` using the filenames listed above.  
3. Open `notebooks/01_ED_Analysis.ipynb` and `notebooks/02_ICU_Sepsis_Analysis.ipynb`.  
4. Update `PROJECT` in each notebook to match your own Google Drive project path, or adapt it for local execution.  
5. Run all notebook cells in order. Outputs should be saved in `data/processed/` and `images/`.  
6. Open the Power BI dashboard in `dashboard/`; if its data-source paths refer to another computer, use Power BI's data-source settings to point to your processed CSV files, then refresh.  
7. Compare notebook metrics with the Power BI model tables and executive report.

## Limitations and responsible use

The ICU clinical variables are synthetic educational data, not genuine patient observations. Missingness, small ICU sample size, train/test-split variation, uncertain availability times of clinical variables, and confounding limit interpretation. Associations must not be interpreted as causes; neither the baseline classification models nor the report should be used to guide patient care.

## Deliverables

- ED and ICU Jupyter notebooks  
- Power BI dashboard (`.pbix`)  
- Executive report (`.pdf`)  
- Supporting chart and confusion-matrix images  
- Repository documentation