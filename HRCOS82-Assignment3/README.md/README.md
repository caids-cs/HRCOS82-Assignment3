# Bridging the Domain Knowledge Gap in E-Learning

A research pipeline for predicting student performance using only pre-assessment behavioural data from a Learning Management System (LMS). 

Developed for the HRCOS82 module at the University of South Africa (UNISA).

The core aim of this project is to compare two intrinsically interpretable machine learning models—Logistic Regression and Decision Trees—to determine which provides better early warning for at-risk students without sacrificing transparency.

| Domain | Entity | Events | Label |
|---|---|---|---|
| **This Project** | a student | LMS behavioural interactions | At-Risk / Pass |

Once the data is written in the canonical behavioural schema (`raisedhands`, `VisITedResources`, `AnnouncementsView`, `Discussion`), one feature builder, one splitting rule, one model set and one evaluation serve both.

---

## Run it in three minutes

You do not need to hunt for the data. It is publicly available on Kaggle and UCI.

**1. Clone the repository and install requirements:**

    git clone https://github.com/YOUR-USERNAME/HRCOS82-Assignment3.git
    cd HRCOS82-Assignment3
    pip install -r requirements.txt

**2. Run the notebook:**

    jupyter notebook notebooks/experiment.ipynb

That produces figures in `results/figures/` and tables in `results/tables/`. 

Other things to try:

    python src/train_models.py
    python src/evaluate.py

---

## What the pipeline enforces

Three rules are built into the code rather than left to your discipline.

**Split before you fit anything.** The `MinMaxScaler` is fitted **only** on the training data, and then applied to the test data. Fitting it on the whole dataset beforehand inflates every number you would then report — it is the most common serious error in this kind of work, and it is invisible in the output.

**Always run a baseline.** A Logistic Regression model is run every time. If a complex model (like a deep neural network) cannot beat Logistic Regression, that is a finding and you must report it, not bury it.

**Never trust accuracy on imbalanced data.** With a 70% At-Risk / 30% Pass split, predicting "At-Risk" for everyone scores 70%. The pipeline prints this majority-class accuracy next to your model's so the comparison is unavoidable, and it reports **Recall** as the primary metric, alongside Precision and F1.

---

## Layout

    notebooks/experiment.ipynb   One notebook, end to end
    data/raw/xAPI-Edu-Data.csv   The raw dataset
    data/processed/              Generated train/test splits
    results/figures/             Confusion matrices, decision tree, bar charts — DO commit these
    results/tables/              The classification metrics table — DO commit these
    README.md                    This file
    requirements.txt             The required Python packages

---

## Data: read this before you add any

**No learner data, personal data or institutional data is ever committed to this repository.** Not to a private one either.

This project relies on the **publicly available xAPI-Edu-Data dataset** (Amrieh, Hamtini, & Aljarah, 2016). It contains no personally identifiable information (PII) and is safe to share. 

However, if you adapt this pipeline to use real institutional data in the future, raw data must live in a secure location. `data/raw/` is git-ignored so that an accidental `git add .` cannot publish sensitive data. 

If you believe you have committed data by mistake, stop and tell your supervisor immediately. Do not simply delete the file — git keeps the history.

---

## Using it for your own project

Do not modify the core preprocessing or evaluation logic to fit your data. Write a small adapter that converts your data into the canonical schema (the four behavioural columns), put it in `src/`, and leave the rest alone. That is what makes your results comparable with the rest of the cohort — and comparability is what turns a set of separate projects into a research programme.

Add your own models to the notebook, but **keep the baselines**. 

---

## Citing this

If you use this pipeline or the findings in a dissertation or a paper, cite the original dataset author and this repository:

    Amrieh, E. A., Hamtini, T., & Aljarah, I. (2016). Mining educational data to predict 
    student’s academic performance using ensemble methods. International Journal of 
    Database Theory and Application, 9(8), 119–136.



## Licence

MIT. See `LICENSE`.
