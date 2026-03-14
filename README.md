# MDS4: Data Science Applications – Final Project

**Dataset:** Hospital Patient Records (Diabetes 130-Hospitals)  
**Author:** [Hasan Mohammad Noman]  
**Date:** [14/03/2026]

## Overview

This project focuses on predicting hospital readmissions for diabetic patients within 30 days of discharge. The goal is to help hospital care coordination teams allocate limited follow-up resources effectively to prevent avoidable readmissions.

## Problem Statement

- **Stakeholder:** Hospital Care Coordination and Planning Team
- **Scenario:** Allocate limited follow-up resources (e.g., transition-of-care phone calls, home visits) to diabetic patients at high risk of avoidable readmissions
- **Prediction Task:** Binary classification (readmitted <30 days [Target=1] vs. other [Target=0])
- **Prediction Time:** At the exact moment of patient discharge (no data leakage from post-discharge events)

## Dataset

The project uses the Diabetes 130-Hospitals dataset, which includes:
- Patient demographics
- Clinical measurements
- Hospital admission details
- Discharge information

Files:
- `data.csv`: Main patient records
- `mappings.csv`: Code mappings for categorical variables

## Methodology

### Data Preprocessing
- Handle systematic missingness (replace '?' with NaN)
- Remove high-null columns (>30% missing)
- Prevent data leakage by excluding deceased/hospice patients
- Stratified 80/20 train-test split to maintain class balance

### Feature Engineering
- Numeric features: Median imputation + StandardScaler
- Categorical features: Constant imputation ('missing') + OneHotEncoder
- Pipeline-based preprocessing to prevent data leakage

### Models
1. **Baseline:** Logistic Regression (interpretable)
2. **Strong Model 1:** Random Forest Classifier
3. **Strong Model 2:** Gradient Boosting Classifier

All models use class-weight balancing for the imbalanced dataset (~11% positive class).

### Evaluation
- Primary metric: Recall (critical for missing high-risk patients)
- Error analysis: Age-based bias check (patients >70)
- Threshold tuning: Lower to 0.35 for better recall-precision trade-off

## Installation

## Setting up the environment

Set up a local environment once so you can install the packages from `requirements.txt` and run the notebooks smoothly.

### Prerequisites

- **Python 3.10 or 3.11** (recommended). Check with: `python3 --version`
- **pip** (usually included with Python). Check with: `pip --version`

### Step 1 — Clone or download the repository

```bash
cd /path/to/your/projects
git clone <repository-url>
cd xu-mds6-case-study-lab-template
```

Or download and unzip the repo, then open a terminal in the project root (the folder that contains `src/`, `requirements.txt`, and the notebooks).

### Step 2 — Create and activate a virtual environment

Using a virtual environment keeps this project’s dependencies separate from your system Python.

**On macOS / Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```
## Remark: .venv is the name you choose for this environment, you can also choose some other name for it

**On Windows (Command Prompt):**

```cmd
python -m venv .venv
.venv\Scripts\activate.bat
```

**On Windows (PowerShell):**

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

You should see `(.venv)` (or similar) in your prompt. The rest of the steps assume this environment is activated.

**Optional — using Conda:**

```bash
conda create -n mds6-lab python=3.11 -y
conda activate mds6-lab
```

### Step 3 — Install dependencies

From the **project root** (same directory as `requirements.txt`):

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

This installs: `numpy`, `pandas`, `scikit-learn`, and `matplotlib` (and their dependencies).

### Step 4 — Verify the installation

Check that the main packages are available:

```bash
python -c "import numpy, pandas, sklearn, matplotlib; print('All packages OK')"
```

If you see `All packages OK`, the environment is ready.



---


## Usage

Run the Jupyter notebook `Dataset_C_Hospital_Patient_Records.ipynb` to:
- Load and preprocess data
- Train models
- Evaluate performance
- Analyze results

## Key Findings

- Random Forest with custom threshold (0.35) recommended for deployment
- Significant age bias detected: poor recall for elderly patients
- Ethical considerations: avoid automation bias, integrate SDOH data

## Limitations & Future Work

1. **Missing SDOH:** No socioeconomic factors included
2. **Class Imbalance:** Consider SMOTE for oversampling
3. **Bias Mitigation:** Further investigation of demographic biases needed

## Ethical Considerations

- Age-based bias in model predictions
- Risk of automation bias overriding clinical judgment
- Importance of human oversight in high-stakes healthcare decisions