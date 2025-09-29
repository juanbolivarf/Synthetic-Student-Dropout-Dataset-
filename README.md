# Synthetic-Student-Dropout-Dataset-
This dataset is synthetic and created for educational purposes (EDA, cleaning, feature engineering, supervised vs. unsupervised discussion), as this take part of a Computer Engineering's undergrade Data mining coursework activity. This is presented by student Juan Bolívar Ferrer.

Records: 1,000
Target: dropout (1 = drops out during first academic year, 0 = persists)
Purpose: Early-warning modeling for student retention (supervised classification), plus robust data-cleaning practice (nulls + outliers intentionally injected).

1) Files in this repository
.
├── dropout_synthetic.csv          # The dataset (1,000 rows)
├── README.md                      # This document
└── generate_dataset.ipynb / .py  # Code to regenerate

2) Dataset schema (variables, types, ranges)


<img width="816" height="696" alt="image" src="https://github.com/user-attachments/assets/8a444428-4673-46d3-8027-8d8d2289919e" />


* Ranges above are the intended domain; outliers intentionally violate some natural bounds to force cleaning decisions.

3) How nulls and outliers were introduced (for cleaning practice)
Nulls (MAR/MNAR mix)

We injected missing values at controlled rates to simulate real pipeline issues:

first_sem_gpa: 10% — common scenario when the first term is not fully observed.

age: 5%

hs_gpa: 3%

admission_score: 2%

socioeconomic_level: 2%

scholarship, loan, financial_aid: 1% each

The selection of rows to null is random, using a fixed RNG seed for reproducibility.

Outliers

We deliberately placed unrealistic/extreme values to stress-test cleaning and robust modeling:

Age: injected values like −3, 2, 60, 80, 100 (beyond typical university ages).

HS GPA: injected values like −1.0, 5.8, 6.5, 7.0, 9.0 (outside the 0–5 scale).

Admission Score: injected values like −10, −25, 125, 130, 140, 200 (outside the 0–100 scale).

A total of 18 rows receive these extreme values (6 in age, 6 in hs_gpa, 6 in admission_score), chosen at random with a fixed seed.

4) How the target dropout was generated (logistic DGP)

We compute a latent score 
𝑧
z per student based on plausible relationships, then sample dropout ~ Bernoulli(sigmoid(z)). Signs are chosen to reflect common risk patterns:

Higher risk: lower GPA/scores, lower SES, Rural origin, Loan = Yes, older age

Lower risk: Female, Scholarship = Yes, Financial Aid = Yes


