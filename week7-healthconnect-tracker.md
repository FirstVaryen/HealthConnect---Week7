# HealthConnect Week 7: Data Analytics Track Tracker

**Deadline:** Sunday, 20th September 2026, 11:59 PM WAT
**Track:** Data Analytics
**Last updated:** after adding KPI 5, the distance redundancy check and the Logistic Regression retest, and rebuilding the PDFs into the Week 6 folder structure

---

## 1. Week 6 to Week 7 Transition write-up
- [x] All six required elements written (report Section 1)

**Status: DONE.**

---

## 2. Part 1: Testing Readiness & Execution
- [x] KPI 1 to 4 reconciled against the dashboard and source CSVs: exact match
- [x] Independent recompute of the 4 dashboard KPIs from the prepared CSV: matched to 4 decimal places
- [x] KPI 5 (cancellation-to-no-show ratio) reproduced against the Week 6 report: all point estimates match
- [x] Lead-time finding segment-tested against appointment_type (4 types) and age_group (6 groups): holds in all
- [x] Distance band CI overlap check: 3 middle bands statistically indistinguishable
- [x] Distance vs lead-time redundancy: not redundant (correlation -0.008), 15+ km gap inside every lead band, about +7 points overall
- [x] Double-risk segment reproduced and root-caused (first attempt 2.46% / 82.1%; correct definition lead 31+ days and prior no-shows 2+: 4.66% / 73.0%)
- [x] Double-risk bootstrap stability: 95% CI [67.4%, 79.0%]
- [x] Formal test table in report Section 3

**Status: DONE.**

---

## 3. Refinement identified from testing
- [ ] Distance chart visual refinement applied in the live `.pbix` (mockup exists: `outputs/dashboard/distance_chart_refinement_mockup.png`)
- [ ] Live dashboard re-exported (the "after" screenshot, save in `outputs/dashboard/`)
- [ ] Re-test after refinement (confirm chart now reads correctly)

**Status:** Guidance ready, not yet done in the real dashboard. The dashboard file to edit is in `week 6\outputs\dashboard\`.

---

## 4. HC-POD Cross-Track Testing (mandatory, at least 1)
- [x] DS track collaborator's `double_risk_flag` (train_improved.py) tested against the DA-validated finding
- [x] Full loop documented: test, finding, action, retest, validated improvement (report Section 6)
- [x] Retested under Random Forest (0.6661 vs 0.6662) and the exact Week 6 candidate Logistic Regression (0.6819 vs 0.6821; no flag 0.6820) via scripts/week7_double_risk_exact_candidate_test.py
- [x] Decision: keep 31+ days (233 patients at 73.0% vs 123 at 82.1% for 46+)
- [x] Week 6 Decision Support text also cites 46+ days: noted as superseded in the report and notebook
- [ ] Optional: copy the two evidence CSVs to the DS track collaborator's repo folder
- [ ] DS track collaborator merges the corrected threshold into train_improved.py and robustness_check.py (Week 8)

**Status: DONE for Week 7.**

---

## 5. Week 7 Project Summary
- [x] Written and rebuilt as `reports/HealthConnect_Week7_Project_Summary.pdf`

**Status: DONE.**

---

## 6. Assumptions, Limitations, Risks & Dependencies
- [x] Resolved vs unresolved issues listed (report Section 8)
- [x] Double-risk call pilot design written (report Section 9), not run

**Status: DONE.**

---

## 7. Submission Package
- [x] Report, Project Summary and Manifest rebuilt as PDFs in `reports/`
- [x] Executed notebook in `notebooks/` (new sections 1b, 3b, 5b run with real outputs)
- [x] Evidence: `reports/cross_track_evidence/`, `reports/test_evidence/`, `scripts/`
- [x] Folder structure matches Week 6 (plus `scripts/`), `README.md` and `.gitignore` in place
- [ ] Live-dashboard export after the distance-chart fix
- [ ] README: add Drive folder link and social post links
- [ ] Uploaded to Google Drive, organised, correctly named
- [ ] GitHub repo updated, commit made

**Status:** Package built, waiting on the dashboard export and the upload/commit.

---

## What's actually left (in priority order)
1. **Apply the distance chart refinement in Power BI and re-export** (Section 3)
2. **Check the rebuilt PDFs once by eye**, then upload to Drive and commit to GitHub (Section 7)
3. **Add the Drive and social links to README.md** after submitting

Old versions of the three PDFs, the tracker, notebook and evidence CSV are in `_backup_before_restructure/`. Delete that folder before committing to GitHub.


---

## 8. Added after checking the brief (Sections 8B, 9, 12, 13)
- [x] Testing record in the brief's 11-field format: `reports/Week7_Testing_Validation_Record.pdf` and `.csv`
- [x] Limitations table with impact and mitigation (report Section 8)
- [x] Validated findings for the wider solution (report Section 10) and Week 8 recommendations (Section 11)
- [x] KPI 5 confirmed ON the dashboard (bottom-right chart, no error bars): documents corrected
- [x] Power BI steps written: `outputs/dashboard/Power_BI_Refinement_and_Slicer_Steps.md`
- [x] Expected slicer values: `reports/test_evidence/dashboard_filter_expected_values.csv`
- [x] Handoff package built: `handoff/ds_track_collaborator/`
- [ ] Apply chart refinement, add slicers, test them, export the after screenshot (user, in Power BI)
- [ ] Send the handoff package and save the screenshot in `handoff/ds_track_collaborator/evidence/` (user)
- [ ] Fill the PENDING rows in the testing record, then rebuild with `python _session_handoff\build_pdfs.py`
- [x] Open questions answered: keep the "DS track collaborator" wording; flag test re-run on the exact Week 6 candidate (done, no difference)
- [x] Documents, PDFs, notebook and posts updated to report the exact-candidate result
- [ ] Social posts: drafts in `_session_handoff/social_posts_draft.md`

Full step-by-step state for any new session: `_session_handoff/CHECKLIST.md`.
