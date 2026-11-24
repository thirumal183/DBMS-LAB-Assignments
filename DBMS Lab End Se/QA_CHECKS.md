# Final QA and validation log

Checked against the supplied question paper and source files on 24 November 2026. Final academic cover details: NIT Warangal; Thirumal; 24MAB0A25; Database Management Systems (DBMS); course instructor Dr. Vikas Srivastava.

## Structural checks
- The deck contains 17 slides: slides 1–8 are the Product Director readout (within the stated maximum of 8); slides 9–17 are the supporting appendix.
- The PDF export is rebuilt from the PowerPoint after the final corrections; it contains 17 pages.
- All PowerPoint shapes are within slide boundaries. The channel and ARPDAU appendix charts were resized to remove overlaps with text and tables.
- The ZIP contains the deck, PDF, SQL, scripts, charts, results and all five CSV datasets.
- Cover includes student/institution/course/instructor details; the first 8 slides remain within the Product Director readout limit, with slides 9–17 as appendix.

## Source-data checks
- All three supplied XLSX files have matching headers and row counts against their CSV conversions: player_day 667,435; currency_spend 489,892; ad_view 647,623.
- Re-running the PDF reconstruction script reproduces player_profile.csv (80,295 rows) and purchase.csv (15,426 rows) byte-for-byte.
- All 11,054 non-null profile first_purchase_date values match the earliest positive purchase event date for the same device.
- player_day has zero duplicate (device_id, activity_date) rows.

## SQL checks
- All 14 executable SQL statements in sql/dbms_queries.sql execute successfully in the generated SQLite database. The SQL repeat-purchase median and quartiles agree with the Python results (approximately 14.98, 5.73 and 32.02 days).
- Core counts agree with the analysis outputs: 80,295 profiles; 667,435 player-days; 15,426 purchase events; 489,892 currency-spend events; 647,623 ad events.

## Numerical and editorial corrections made during this review
- Platform payer share in the analysis notes corrected to the player-day-weighted values: Android 1.43%, iOS 2.86%.
- The executive ARPDAU decline title corrected from 16.5% to 16.3%.
- Appendix ARPDAU counterfactual corrected to $0.3851 (+8.0%) at January's active-player mix; actual April ARPDAU is $0.2985.
- Channel adjusted revenue labels corrected from “net” to “gross”; the model uses positive gross purchase revenue per install.
- Churn top-decile precision/waste figures aligned to the computed values: 45.5% precision and 54.5% non-churners.
- Churn ROC-AUC consistently rounded to 0.697.

## Interpretation boundaries retained
- The ARPDAU decomposition is descriptive, not causal.
- Channel comparisons are observational and cannot establish incremental marketing ROI without spend/CPI or randomization.
- Churn risk is not offer-response uplift; an experiment with a holdout is required.
- The sales-frequency analysis (2b) and optional 90-day value model (4b) are explicitly identified as not selected.

## Final regeneration checks
- Re-ran descriptive analysis, churn training, chart generation and PowerPoint generation from the packaged source files; each component completed.
- Re-exported the 17-slide PowerPoint to PDF and visually reviewed the full slide montage plus representative detail slides (cover, channel comparison and data-quality appendix).
- Loaded all five CSVs into SQLite and executed all 14 semicolon-delimited SQL statements after removing comments; zero SQL errors.
