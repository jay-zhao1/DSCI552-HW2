# DSCI 552 - Homework 2

**Yang Zhao** | **USC NetID:** yzhao528

Analysis of the Combined Cycle Power Plant dataset, plus ISLR Chapter 2 exercises 1 and 7.

## Repository contents

```text
.
├── README.md
├── requirements.txt
├── .gitignore
├── DSCI552_Homework2_Yang_Zhao.ipynb
├── DSCI552_Homework2_Yang_Zhao.pdf
└── CCPP/
    ├── Folds5x2_pp.xlsx
    └── Readme.txt
```

The notebook contains the executable analysis, written answers, tables, and saved plots. The PDF is the accompanying written report. Only Sheet1 of the Excel workbook is used: 9,568 observations, four predictors (AT, V, AP, RH), and response PE. AT and PE correspond to T and EP in the assignment. The other workbook sheets are shuffled versions of the same data and are not combined. No observations are deleted or imputed.

## Setup and execution

Tested with **Python 3.13.5**. Package versions are pinned in `requirements.txt`.

From the repository root:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m ipykernel install --user --name dsci552-hw2 --display-name "Python (DSCI552 HW2)"
python -m jupyter lab
```

On Windows, activate the environment with `.venv\Scripts\activate` instead of `source .venv/bin/activate`.

Open `DSCI552_Homework2_Yang_Zhao.ipynb`, select the **Python (DSCI552 HW2)** kernel, and run **Restart Kernel and Run All Cells**. Save the notebook afterward. Keep the notebook in the repository root so its relative data path `CCPP/Folds5x2_pp.xlsx` resolves correctly.

To execute and save all outputs without opening the notebook UI, after setup run:

```bash
python -m jupyter nbconvert --to notebook --execute --inplace --ExecutePreprocessor.kernel_name=dsci552-hw2 --ExecutePreprocessor.timeout=600 DSCI552_Homework2_Yang_Zhao.ipynb
```

All computational tables and plots are reproduced by the notebook. The supplied PDF is a separately formatted report; notebook execution does not regenerate the PDF.

## Reproducibility and results

Parts (h)-(j) use the same 70/30 train/test split with `random_state=42`. Scaling parameters are estimated on the training set only. Backward elimination preserves main effects required by retained squares or interactions. KNN uses uniform weights and Euclidean distance; "normalized" features are z-score standardized with `StandardScaler`.

| Model | Best k | Train MSE | Test MSE |
|---|---:|---:|---:|
| All-predictor linear regression | - | 20.5808 | 21.2399 |
| Selected quadratic + interactions | - | 17.8908 | 18.6600 |
| Raw-feature KNN | 5 | 10.6008 | 15.7268 |
| Standardized-feature KNN | 4 | 8.5914 | 14.3057 |

The best k is selected by the plotted test MSE, following the exercise. This minimum is a model-selection result, not an independent final evaluation. A new predictive study should use validation or cross-validation to select k before final testing.

## Data source

[UCI Combined Cycle Power Plant dataset](https://archive.ics.uci.edu/dataset/294/combined+cycle+power+plant). The original dataset description and associated research references are included in `CCPP/Readme.txt`.
