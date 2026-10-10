# DS310 Regression Project

Regression modeling for a Penn State Kaggle competition using feature engineering, weighted ridge regression, and model ensembles.

**Final result:** Team 9 placed **1st** with a private leaderboard MSE of **2058.85426**.

[Competition and leaderboard](https://www.kaggle.com/competitions/ds-310-fall-2026-project-1) · [Notebook](analysis/regression_analysis.ipynb) · [Report](report/regression_report.pdf)

Completed for DS 310 at Penn State in Fall 2026.

The goal was to predict the target values for a Kaggle competition. I started with ridge regression, compared other models, and made smaller changes to features, training weights, and model blends.

## Final Result

| Result | Value |
| --- | ---: |
| Final private Kaggle MSE | **2058.85426** |
| Final leaderboard rank (Team 9) | **1** |
| Public Kaggle MSE | **2930.80324** |
| Training rows | 242 |
| Test rows | 200 |
| Supplied predictor columns | 64 |

The final private score and rank were supplied from the competition leaderboard by Michael Shepherd. The report screenshot was taken on October 4, 2026 and records the public leaderboard at that time. Public and private MSE use different evaluation samples and are not directly comparable.

## Approach

The project included:

- Data checks and feature scaling
- Added powers and separate penalties for feature groups
- Weighted ridge regression
- PCA regression, SVR, splines, and shallow tree models
- Model stacking and fixed prediction blends
- Small prediction changes with size limits
- Local validation and comparisons with reported Kaggle scores

The final model uses fixed weights to combine model predictions and smaller changes. Some weights are negative. The final notebook contains the complete recipe and fits the models from the supplied training data.

## Model Results

| Model | Public MSE |
| --- | ---: |
| Ridge using all 64 columns | 3190.60 |
| Weighted ridge with added features | 3051.87 |
| Reference blend with small changes | 3013.40 |
| Blend with feature penalty changes | 2965.97 |
| Blend with residual weights | 2959.83 |
| Earlier signed model blend | 2942.52 |
| Final signed model blend | **2930.80** |

## Repository Structure

```text
analysis/
    regression_analysis.ipynb
assignment/
    README.md
data/
    x_train.csv
    y_train.csv
    x_test.csv
    sampleSubmission.csv
development/
    Versions.zip
    archive_manifest.csv
    README.md
report/
    regression_report.pdf
submissions/
    final_submission.csv
    README.md
requirements.txt
```

- `analysis/` has the finished notebook.
- `report/` has the nine page course report and leaderboard screenshot.
- `data/` has the supplied competition data.
- `submissions/` has the final scored predictions.
- `development/` keeps the older work in one ZIP instead of listing thousands of version files.
- `assignment/` explains the course requirements.

## Run the Notebook

Use Python 3.12 and install the packages:

```bash
python -m pip install -r requirements.txt
```

Open [the final notebook](analysis/regression_analysis.ipynb) and run its cells in order. The notebook can find `data/` when opened from either the project folder or `analysis/`.

The run creates `reproduced/submission.csv`. It checks the 200 row IDs and compares the predictions with the original scored file. The full model run was checked and matched within 0.000001. The sample submission outputs are not used as target labels.

The optional final validation is off for the normal run because it takes longer.

## What I Learned

A bigger model did not always do better. Weighted ridge was a useful starting point. Careful feature penalties and training weights helped more than adding models without a clear reason.

Some changes looked good locally but did worse on Kaggle. The local five fold MSE for the final recipe was **3483.96**, which was different from the public score. I used public scores many times during the search, so the public result is not a fresh test of every model choice. I would keep a separate validation set and use fewer public checks if I repeated the project.

## Tools

Python, Jupyter Notebook, NumPy, pandas, SciPy, and scikit-learn.

## Author

**Michael Shepherd**  
Data Science, Penn State University
