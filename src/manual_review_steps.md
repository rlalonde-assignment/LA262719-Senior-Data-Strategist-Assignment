# Manual Review Steps

The data pack was small enough to review directly in CSV format. I used a manual review approach so the work would remain transparent and proportionate to the assignment scope.

The original source files are preserved in the data folder. Cleaned working files and the risk report are in the output folder.

## Steps followed

1. Reviewed data_dictionary.csv to understand the fields and expected meaning of each source file.

2. Reviewed site_inventory.csv for:
   - valid site_id values
   - non-site rows
   - current labels and descriptors
   - anonymous link indicators
   - external guest counts
   - item counts
   - obvious data quality issues

3. Reviewed pii_detections.csv for:
   - detection type
   - match_count values
   - SIN-related findings
   - site_id alignment with site_inventory.csv

4. Reviewed sharing_links.csv for:
   - anonymous links
   - external sharing domains
   - site_id alignment with site_inventory.csv

5. Reviewed license_assignments.csv for:
   - E7 licence assignment
   - account status
   - service or shared accounts
   - support for the 900-staff eligibility claim

6. Compared the files by site_id to identify sites where sensitive detections, anonymous links, external guests, blank labels, or retired labels overlap.

7. Created cleaned working files in the output folder.

8. Created output/risk_view.md as the main report.

9. Created governance files for label configuration, sample document labels, and the ethics memo.
