# Handoff note: `double_risk_flag` threshold (Data Analytics to DS track collaborator)

**From:** Hillary (Data Analytics track)  **Project:** HealthConnect Clinic, Week 7 cross-track testing

## What I tested
Your `double_risk_flag` feature in `train_improved.py` says in its comment that it encodes the Data Analytics double-risk finding (long lead time plus repeated prior no-shows, about 4.7% of bookings, about 73% no-show rate). I recomputed the segment from the shared prepared dataset (`healthconnect_appointments_prepared.csv`).

## What I found
| Definition | Rule | Bookings | Share of 5,000 | No-show rate |
|---|---|---|---|---|
| Validated (Data Analytics) | lead time >= 31 days AND prior no-shows >= 2 | 233 | 4.66% | 73.0% |
| As coded | lead time >= 46 days AND prior no-shows >= 2 | 123 | 2.46% | 82.1% |
| Left out by the coded version | lead time 31 to 45 days AND prior no-shows >= 2 | 110 | 2.20% | 62.7% |

The coded threshold (46) is narrower than the finding the comment cites. It leaves out 110 patients who share the same stacking effect. The counts above use all 5,000 bookings. Your models drop cancelled bookings, so on the 4,737 rows you train on, the same two rules give 225 patients (75.6%) and 120 patients (84.2%).

## Does it change model performance? No.
- Random Forest, 5-fold cross-validation ROC-AUC: 0.6661 (>= 46) vs 0.6662 (>= 31).
- Your Week 6 candidate model (Logistic Regression on the 12 restricted features from `robustness_check.py`, scaled, balanced classes), rebuilt from your own code: 0.6819 (>= 46) vs 0.6821 (>= 31), and 0.6820 with the flag removed completely. My run reproduces the 0.6819 in your `candidate_model.json`. Over 5 x 5 repeated cross-validation the paired difference is +0.0001 (31+ wins 13 of 25 folds).

So this is a documentation/consistency fix, not a performance fix. The Random Forest already learns the interaction from the raw features, and your Logistic Regression already has the `leadtime_x_priornoshow` term, which is why the flag adds nothing either way. Files: `crosstrack_double_risk_flag_retest_evidence.csv` (Random Forest), `crosstrack_double_risk_flag_exact_candidate_retest_evidence.csv` (your Week 6 candidate, with the run log `double_risk_exact_candidate_test_output.txt`; this replaces my earlier simplified check in `crosstrack_double_risk_flag_lr_retest_evidence.csv`), `double_risk_flag_segment_comparison.csv` (the table above).

## What I am asking you to do
1. In `train_improved.py` and in `build_restricted_features` in `robustness_check.py` (the code your Week 6 candidate was selected from, which has the same >= 46 rule), change the flag to `double_risk_flag = (booking_lead_days >= 31) & (previous_no_shows >= 2)` and update the comment so the code, the comment and the 4.66% / 73.0% figures agree.
2. Tell me once it is merged (or if you disagree with the ≥ 31 definition), so I can re-run the comparison on your updated pipeline in Week 8.

## Delivery record (fill this in when you send it)
| Field | Entry |
|---|---|
| Sent on (date) | |
| Sent how (WhatsApp, email, Slack, etc.) | |
| Reply received (yes/no, date) | |
| Screenshot saved in `evidence/` as | |
