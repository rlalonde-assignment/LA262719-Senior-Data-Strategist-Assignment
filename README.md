# Senior Data Strategist — Take-Home Submission

Start with `ASSIGNMENT.md`. The sensitivity-label deck (`INFORMATION_PROTECTION.pptx`)
is provided alongside this repository.

## How to run my work
No script is required for this submission.

The source data pack is small enough to review directly. I preserved the original files in the data folder and created cleaned working outputs in the output folder.

To reproduce the work:

1. Review the original CSV files in the data folder.
2. Follow the review steps in src/manual_review_steps.md.
3. Validated the cleaned CSV files in the output folder.
4. Read the main risk report at output/risk_view.md.

## Assumptions
- Findings are based on the supplied assessment files.
- Records with unclear, inconsistent, retired, or missing labels were treated as requiring validation.
- For risk analysis, sites were treated as potentially reachable by Copilot unless excluded from go-live.
- Restricted sites and high-risk sites were held out of go-live where access, sharing, sensitivity, or label confidence was not strong enough.
- External guests, anonymous links, Restricted content, and confirmed sensitive content were treated as priority review areas.
- Formats and data types were inferred from the majority pattern and corrected for consistency.

## What I'd do with more time
With more time, I would prioritize the following:

1. Validate the scan findings with site owners to confirm true positives, false positives, duplicate detections, and stale content.

2. Confirm whether the licence file is a sample or a full extract, then verify the actual number of Copilot-eligible staff.

3. Identify and normalize data quality issues, including text encoding problems, inconsistent date formats, duplicate records, and missing or retired labels.

4. Build a repeatable script to automate the data checks once the required rules and source formats are confirmed.

5. Create a simple report showing label coverage, sensitive-content locations, anonymous links, external guests, and recommended remediation priorities.

6. Review high-risk sites with business owners before changing labels or applying Copilot restrictions.

7. Create a remediation backlog for blank labels, retired labels, anonymous links, external guests, confirmed SIN content, and Restricted content.

8. Develop a Copilot rollout checklist covering access review, label enforcement, user communications, training, exception handling, and post-go-live monitoring.

9. Expand the privacy review into a formal assessment covering FOIPPA considerations, retention, collection authority, disclosure risk, breach response, and governance accountabilities.