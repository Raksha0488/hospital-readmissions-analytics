PROJECT NOTES — Hospital Readmissions Analysis

Dataset: Diabetes 130-US hospitals dataset (1999-2008), 101,766 patient 
hospital admissions. Each row is one hospital visit by a diabetic patient.

What I was trying to figure out:
1. Which age group comes back to the hospital most within 30 days?
2. Does staying longer in the hospital make someone more likely to come back?
3. Does the number of medications a patient is on affect readmission?
4. Do different race groups show different readmission patterns?

Cleaning the data:
Some columns (weight, payer_code, medical_specialty) had a lot of missing 
values, so I dropped them. The race column had some unknown/missing entries 
marked as '?', which I replaced and removed before the cleaning check.

What I found:
About 11.16% of all patients (11,357 out of 101,766) were readmitted within 
30 days. When I first built a prediction model, it showed 88.7% accuracy, 
which sounded good — but I realized that's basically the same as just always 
guessing "not readmitted," since only 11% of patients actually come back. So 
the model wasn't really learning anything useful, just going with the safe 
guess every time.

To fix this, I told the model to pay more attention to the rarer readmitted 
cases instead of just chasing overall accuracy. This dropped the accuracy to 
around 50%, but it got much better at actually catching real at-risk 
patients — correctly identifying about 59% of people who really did get 
readmitted, instead of almost none before.

The two factors most linked to readmission were how many total diagnoses a 
patient had and how long they stayed in the hospital.

What I'd recommend:
Since missing an at-risk patient is probably more costly than making an 
unnecessary follow-up call, I think it makes sense for hospitals to lean 
toward flagging more people as "at risk" even if some of them turn out fine, 
rather than trying to be overly precise and missing real cases.
