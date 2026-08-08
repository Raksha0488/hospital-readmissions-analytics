# hospital-readmissions-analytics

## Problem
Diabetic patients often get readmitted to the hospital within 30 days of 
being discharged, and hospitals actually get penalized financially for 
this because it's seen as a sign that something was missed the first time 
(bad discharge planning, medication issues, etc). I wanted to look at real 
hospital data and figure out what factors are actually linked to this, and 
whether it's something that could be predicted in advance.

## Dataset
Diabetes 130-US Hospitals dataset (1999-2008) from Kaggle — 101,766 patient 
admissions across 130 hospitals in the US. [https://www.kaggle.com/datasets/brandao/diabetes]

## Notebook
Full analysis with code and output:
(https://www.kaggle.com/code/raksharajput0488/diabetic-patient-readmission-analysis)

## Approach
- First explored the data and found a few columns (weight, payer_code, 
  medical_specialty) were mostly missing, so I dropped them. Also cleaned 
  up unknown/missing race entries.
- Wrote SQL queries to check readmission rates against age, length of 
  hospital stay, number of medications, and race.
- Built a Power BI dashboard to actually visualize these patterns instead 
  of just looking at raw numbers.
- Built a logistic regression model to see which factors were the strongest 
  predictors of a patient being readmitted within 30 days.

## Key Findings
Out of the 101,766 admissions, 11.16% (11,357 patients) were readmitted 
within 30 days. My first model gave 88.7% accuracy which looked great at 
first, but I realized this number was basically useless, since only ~11% 
of patients actually get readmitted, a model that just predicts "not 
readmitted" every single time would already score close to 88-89% without 
learning anything at all. So I fixed this by making the model pay more 
attention to the minority (readmitted) cases instead of just optimizing 
for overall accuracy. This dropped accuracy to around 50%, but the model 
got way better at actually catching real at-risk patients going from 
catching almost none to correctly flagging about 59% of them, though it 
also flagged more false alarms in the process. Number of diagnoses and 
length of hospital stay ended up being the strongest predictors of 
readmission out of everything I tested.

## Recommendation
Since missing a patient who's actually at risk is probably worse than 
making an extra follow-up call to someone who turns out fine, I think it 
makes more sense for hospitals to flag more patients as at-risk (based on 
diagnosis count and hospital stay length) even if it means some of those 
flags turn out to be unnecessary.

## Repository Contents
- `notebook.ipynb` — SQL queries, data cleaning, and the prediction model
- `full_dashboard_overview.png` — Power BI dashboard
- `notes.md` — my process notes and the business questions I started with

## Tools Used
SQL, Python (pandas, scikit-learn), Power BI, Excel
