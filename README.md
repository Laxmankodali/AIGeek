# Customer Churn — Exploratory Machine Learning

[View the customer-churn notebook](<cutomer_churn_Linear_LOGISTIC_DT and KNN and SVM and Naivebyes_ENSEMBLE_TECHNIQUE (2).ipynb>)

**Status:** learning/portfolio exploration, not a validated production model. This summary audits the code and saved outputs in notebook blob `aca89d4191fd983a0a8092297129a81fbeb4e2a7`; it does not claim a fresh execution.

## Problem and data assumptions

Explore whether customer demographics, tenure, services, contract and billing attributes can classify `Churn`, potentially supporting retention outreach. A separate linear-regression exercise predicts `TotalCharges`; its results are not churn-classification results.

The notebook loads `Customer_Churn.csv`, which is **not included** in this repository. Saved summaries show 7,043 initial records and 7,026 after cleaning. The schema resembles a telecom customer dataset, but its source, license, collection period, churn definition and prediction horizon are not documented. Treat one row per customer and feature availability before churn as assumptions requiring verification. The original churn-label mapping is not saved; class 1 should be confirmed as churn before business interpretation.

## Feature preparation

The code converts `TotalCharges` to numeric with invalid values coerced to missing, drops rows with any missing value, resets the index, and label-encodes all object columns (including customer ID and target) before splitting. Classification uses the first 21 columns as predictors and the last column as the target. This retains both `customerID` and the added row `index`.

The split is 75% training / 25% test, with `random_state=1111` and no stratification: saved shapes are 5,269 training and 1,757 test rows. `StandardScaler` is fitted on training predictors and applied to test predictors.

## Evaluation and supported model comparison

These are **saved notebook outputs**, not independently reproduced benchmarks. Cell numbers below are one-based positions, including Markdown and empty cells.

| Model / task | Saved evidence | Interpretation |
| --- | --- | --- |
| Logistic regression / churn | Accuracy **80.31%**; class-1 precision **0.68**, recall **0.55**, F1 **0.61** (cells 49–52) | Confusion matrix: `[[1143,124],[222,268]]`; higher accuracy of the two classifiers with saved scores. |
| Decision tree / churn | Accuracy **74.10%**; confusion matrix `[[955,312],[143,347]]` (cells 58–63) | Class-1 recall **70.82%**, calculated from the matrix: 347/490. More positives detected, but more false positives than logistic regression. |
| Random forest, KNN, linear/RBF SVM, Gaussian Naive Bayes / churn | Code present; no saved evaluation outputs | Performance and relative ranking are unverified. |
| Bagging and AdaBoost / churn | Fit cells 120 and 129 save `NameError: name 'X_train' is not defined` | These saved attempts failed; downstream scores are not established. |
| Linear regression / TotalCharges | RMSE **701.27**, R² **0.9055** (cells 32–33) | Separate regression task; R² is not classification accuracy. Predictors include Churn and identifiers. |

The test report contains 1,267 class-0 and 490 class-1 records; always predicting class 0 would yield **72.11%** accuracy (calculated, not a fitted baseline). Accuracy alone is therefore insufficient. For retention, evaluate positive-class precision, recall, F1 and the confusion matrix against outreach cost and missed-churn cost; no business acceptance threshold is established.

The tree's saved “ROC AUC” of **0.7310** uses hard predictions rather than probability scores. Several later AUC calls also reverse the true-label/prediction arguments. Recompute ROC AUC and PR AUC from probabilities or decision scores with correct argument order. The final comparison table has no saved output, so the notebook's **“Random Forest is best” statement is unsupported**. No overall winning model is established.

## Limitations and reproducibility

- Encoders are fitted before the split; nominal categories receive arbitrary numeric ordering. Identifiers and row index can introduce spurious patterns. Dropping incomplete records may bias the sample.
- Decision-tree, random-forest and KNN searches use all `X,y`, including the designated test rows. The saved tree search returns parameters, but no independent tuned-model evaluation. SVM tuning uses training data, with scaling already fitted outside its CV folds.
- All code execution counts are null despite some saved outputs, so a clean sequential run is not demonstrated. Python metadata says 3.8.5 while a saved warning references Python 3.11; dependency versions are unpinned.
- Colab upload saves the file as `Customer_Churn.csv`, while the read call expects `/content/sample_data/Customer_Churn.csv`. Supply the authorized original CSV and align that path before running. Required imports include pandas, NumPy, seaborn, Matplotlib and scikit-learn; local Jupyter also requires replacing the Colab-only upload cell.
- Restart the kernel and run all cells in order after fixing prerequisites. Record data provenance/checksum, label mapping, Python/package versions and seeds. This documentation review did not rerun training because the CSV is absent.
- No temporal/external validation, probability calibration, fairness assessment, deployment or measured retention impact is demonstrated.

## Practical next steps

1. Document the data source, permitted use, schema, churn horizon and label mapping; verify customer uniqueness and pre-outcome feature timing.
2. Remove identifiers/index, select columns by name, and build train-only preprocessing with a `ColumnTransformer`/`Pipeline`: missing-value handling, one-hot categorical encoding and numeric scaling where appropriate.
3. Reserve an untouched stratified test set (or a time-based holdout when timestamps are available). Tune only within training folds and seed stochastic models.
4. Repair the failed cells, rerun every candidate and publish one comparable results table with a dummy baseline, class-1 precision/recall/F1, probability-based ROC/PR AUC and uncertainty across folds.
5. Choose a threshold using retention economics and capacity, then validate calibration, segment performance and prospective business impact before a monitored pilot.

---

# 💫 About Me:
I'm a Senior Business Intelligence Developer  with 10+ years of experience in the Data and Analytics space.<br>Recently I'm more into Data Engineering and AI Space.


## 🌐 Socials:
[![Bluesky](https://img.shields.io/badge/bluesky-0285FF?style=for-the-badge&logo=bluesky&logoColor=%23FFFFFF)](https://bsky.app/profile/AIGeek) [![email](https://img.shields.io/badge/Email-D14836?logo=gmail&logoColor=white)](mailto:laxmankodali@gmail.com) 

# 💻 Tech Stack:
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![MicrosoftSQLServer](https://img.shields.io/badge/Microsoft%20SQL%20Server-CC2927?style=for-the-badge&logo=microsoft%20sql%20server&logoColor=white) ![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E) ![Google Cloud](https://img.shields.io/badge/GoogleCloud-%234285F4.svg?style=for-the-badge&logo=google-cloud&logoColor=white) ![Azure](https://img.shields.io/badge/azure-%230072C6.svg?style=for-the-badge&logo=microsoftazure&logoColor=white) ![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white) ![Apache Airflow](https://img.shields.io/badge/Apache%20Airflow-017CEE?style=for-the-badge&logo=Apache%20Airflow&logoColor=white) ![Canva](https://img.shields.io/badge/Canva-%2300C4CC.svg?style=for-the-badge&logo=Canva&logoColor=white) ![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white) ![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white) ![scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white) ![TensorFlow](https://img.shields.io/badge/TensorFlow-%23FF6F00.svg?style=for-the-badge&logo=TensorFlow&logoColor=white) ![Matplotlib](https://img.shields.io/badge/Matplotlib-%23ffffff.svg?style=for-the-badge&logo=Matplotlib&logoColor=black) ![Keras](https://img.shields.io/badge/Keras-%23D00000.svg?style=for-the-badge&logo=Keras&logoColor=white) ![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white) ![Power Bi](https://img.shields.io/badge/power_bi-F2C811?style=for-the-badge&logo=powerbi&logoColor=black) ![Portfolio](https://img.shields.io/badge/Portfolio-%23000000.svg?style=for-the-badge&logo=firefox&logoColor=#FF7139)
# 📊 GitHub Stats:
![](https://github-readme-stats.vercel.app/api?username=Laxmankodali&theme=dark&hide_border=false&include_all_commits=false&count_private=false)<br/>
![](https://nirzak-streak-stats.vercel.app/?user=Laxmankodali&theme=dark&hide_border=false)<br/>
![](https://github-readme-stats.vercel.app/api/top-langs/?username=Laxmankodali&theme=dark&hide_border=false&include_all_commits=false&count_private=false&layout=compact)

### ✍️ Random Dev Quote
![](https://quotes-github-readme.vercel.app/api?type=horizontal&theme=radical)

---
[![](https://visitcount.itsvg.in/api?id=Laxmankodali&icon=0&color=0)](https://visitcount.itsvg.in)

<!-- Proudly created with GPRM ( https://gprm.itsvg.in ) -->
