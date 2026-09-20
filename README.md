# HealthConnect Clinic - Week 7 (Data Analytics Track)

**Programme:** AnalystLab Africa Experience Lab
**Project:** Improving Patient Appointment Attendance and Healthcare Support Using Data and AI
**Track:** Data Analytics
**Prepared by:** Hillary Emmanuel
**Week 7 focus:** Analytics Testing & Refinement (test and validate the Week 6 dashboard and findings end to end, plus a cross-track test with the DS track collaborator)

**Google Drive submission folder:** to be added after upload

**Week 7 published social posts:** to be added after publishing

---

## What's in this repository

| Path | What it is |
|---|---|
| `reports/HealthConnect_Week7_Analytics_Testing_Refinement_Report.pdf` | Main Week 7 deliverable: transition write-up, test table, dashboard evidence, distance refinement status, HC-POD cross-track record, business insights, limitations, Week 8 pilot design |
| `reports/HealthConnect_Week7_Project_Summary.pdf` | The Week 7 Project Summary |
| `reports/Week7_Evidence_and_Supporting_Files_Manifest.pdf` | Packing list mapping each submission requirement to its file |
| `reports/cross_track_evidence/` | Evidence for the cross-track test of the DS track collaborator's `double_risk_flag`: Random Forest retest CSV, exact Week 6 candidate (Logistic Regression) retest CSV and run log, plus an earlier preliminary simplified-model check |
| `reports/test_evidence/kpi5_and_distance_checks_output.txt` | Run log for the KPI 5 reproduction and the distance checks |
| `reports/Week7_Testing_Validation_Record.pdf` / `.csv` | The testing record in the brief's 11-field format (all rows complete) |
| `reports/test_evidence/dashboard_filter_expected_values.csv` | Correct values for every slicer selection, computed from the data, for testing the dashboard filters |
| `handoff/ds_track_collaborator/` | Note, evidence CSVs and delivery record for the DS track collaborator (the screenshot of the sent message goes in `evidence/`) |
| `notebooks/HealthConnect_Week7_Testing_Refinement.ipynb` | Executed notebook reproducing every Week 7 test with real outputs |
| `scripts/week7_kpi5_and_distance_checks.py` | KPI 5 reproduction, distance vs lead-time checks, Logistic Regression with and without distance |
| `scripts/week7_double_risk_exact_candidate_test.py` | Double-risk flag threshold retest (46+ vs 31+ vs no flag) on the exact Week 6 candidate model, built by importing the Week 6 data science track code (reproduces its 0.6819 cross-validated AUC). The path to the Week 6 folder is set at the top of the script; edit it if you run this elsewhere |
| `scripts/week7_double_risk_lr_test.py` | Earlier preliminary check on a simplified two-feature Logistic Regression, superseded by the exact-candidate test |
| `outputs/dashboard/Power_BI_Refinement_and_Slicer_Steps.md` | Click-by-click steps for the distance-chart refinement, the slicers and the slicer tests |
| `outputs/dashboard/HealthConnect_Week6_Dashboard_baseline.png` | The dashboard that was tested against (Week 6 build) |
| `outputs/dashboard/distance_chart_refinement_mockup.png` | Before/after design mockup for the distance chart (design reference, not the live dashboard) |
| `data/processed/` | Read-only copies of the prepared dataset and the four Week 6 KPI confidence-interval tables |

Unlike Week 6, this folder has a `scripts/` directory, because several of the checks were run as standalone scripts as well as inside the notebook.

**Dashboard slicers:** three dropdown slicers (appointment_type, age_group, reminder_sent) were added and tested. All card values matched expected figures exactly across T0–T3. CI error bars are static and do not respond to slicers; documented as a limitation in the report.

**Distance-chart colour refinement:** deferred to Week 8. Values and annotation are correct; bar colour differentiation not applied to the live dashboard.

---

## Reproducing the analysis

Any Python 3 environment with `pandas`, `numpy` and `scikit-learn` works (developed on Python 3.14).

```bash
pip install pandas numpy scikit-learn jupyter
cd notebooks
jupyter notebook
```

Open `HealthConnect_Week7_Testing_Refinement.ipynb` and run all cells top to bottom. It reads the prepared dataset from `../data/processed/` read-only.

To run the standalone scripts:

```bash
cd scripts
python week7_kpi5_and_distance_checks.py
python week7_double_risk_lr_test.py
python week7_double_risk_exact_candidate_test.py
```

---

## Headline findings

- **All five KPIs reproduce.** The four dashboard KPIs match their source CSVs exactly, and the cancellation-to-no-show ratio (KPI 5, the bottom-right chart) matches the Week 6 report to three decimals.
- **The double-risk segment stays defined as lead time 31+ days and 2+ prior no-shows** (233 of 5,000 bookings, 73.0% no-show rate). The DS track collaborator's code used 46+ days (123 bookings, 82.1%). The threshold makes no measurable difference to model performance under the Random Forest (0.6661 vs 0.6662) or the exact Week 6 candidate Logistic Regression (0.6819 vs 0.6821, and 0.6820 with no flag at all), so this is a documentation fix. On the 4,737 attended and no-show bookings the model uses, the counts are 225 (75.6% no-show) and 120 (84.2%), because cancelled bookings are excluded from modelling. The Week 6 Decision Support text also cites 46+ days; that wording is superseded.
- **Distance is not redundant with lead time.** The two are unrelated (correlation -0.008), and patients 15+ km away have a higher no-show rate inside every lead-time band (about +7 points overall). The effect is real but modest, so distance stays framed as a 15+ km threshold effect.
- **Long lead-time bookings fail mostly through silent no-shows.** The cancellation-to-no-show ratio falls from about 0.20 (0-7 days) to about 0.08 (46-60 days).

## Open items (carrying into Week 8)

- Apply the distance-chart bar colour refinement in the live Power BI dashboard and re-export it.
- The DS track collaborator still needs to merge the corrected threshold into `train_improved.py`.
- The double-risk call pilot is designed (report Section 9) but not run.
- Google Drive submission folder: to be added after upload.

See `reports/HealthConnect_Week7_Analytics_Testing_Refinement_Report.pdf` for the full write-up.
