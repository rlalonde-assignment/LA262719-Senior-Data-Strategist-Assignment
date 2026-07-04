# Risk Report

All analysis was completed using Excel and Notepad++ through manual inspection and comparison of the provided datasets. This approach was appropriate because the datasets were relatively small and the assessment focused on validating the original files rather than building an automated pipeline.

## Purpose

This report shows label coverage across the site inventory and identifies where Copilot may be able to reach sensitive or over-shared content. The view compares the corrected versions of:

* `site_inventory.csv`
* `pii_detections.csv`
* `sharing_links.csv`

The analysis is site-based and does not rank or target individual staff members.

## Method

The corrected `site_inventory.csv` was used as the base file because it contains the site list, current label information, and ownership.

The `pii_detections.csv` file was grouped by `site_id` to show where sensitive personal information was detected.

The `sharing_links.csv` file was grouped by `site_id` to show where anonymous links, external sharing, or other broad access indicators exist.

The files were compared using `site_id` as the common key.

## Comparison logic

| Question | Source file | Handling |
|---|---|---|
| What sites exist? | `site_inventory.csv` | Used as the base site list. |
| What label is currently applied? | `site_inventory.csv` | Used to assess label coverage and gaps. |
| Where was sensitive personal information detected? | `pii_detections.csv` | Grouped by site and joined to the site inventory. |
| Where are sharing risks present? | `sharing_links.csv` | Grouped by site and joined to the site inventory. |
| Where could Copilot reach sensitive or over-shared content? | All three files | Identified sites that are potentially reachable by Copilot and also contain sensitive content, weak labels, anonymous links, or external access. |

## Label coverage view

| Label status | Number of sites | Notes |
|---|---:|---|
| Public | `2` | Sites or files intended for public release. |
| Internal | `8` | Routine Assembly business content. |
| Confidential | `3` | Sites currently labelled Confidential under the Assembly standard. |
| Restricted | `3` | Highly sensitive content requiring strict need-to-know access. |
| Blank or missing label | `2` | Requires owner review before Copilot inclusion. |
| Retired or invalid label | `6` | Requires correction before Copilot inclusion. |

## Sensitive and Copilot-reachable content

| Site ID | Site name | Current label | PII detected | Risk note |
|---|---|---|---:|---|
| `S-003` | HR Benefits Enrolment | Confidential / All Employees | `622` | Significant HR-related PII with broad label wording and external guest access requires review before go-live. |
| `S-004` | Finance Draft Budgets | Highly Confidential / Specific People | `77` | Non-standard label requires validation and remapping before Copilot inclusion. |
| `S-005` | Hansard Broadcast Ops | Internal | `150` | Internal site contains PII and has anonymous links and external guests. |
| `S-006` | Legal Opinions Library | Restricted | `33` | Restricted legal content contains PII and has anonymous links and external guests. |
| `S-008` | Vendor Contracts (active) | Confidential / Anyone (not protected) | `55` | Confidential vendor content is not protected and has external guest access. |
| `S-009` | IT Security Runbooks | Confidential | `8` | Security content contains PII and should be validated before Copilot inclusion. |
| `S-012` | Constituency Office Files | Confidential / Trusted People | `506` | Constituency files contain significant PII and external guest access. |
| `S-014` | Payroll Records | Highly Confidential / All Employees | `152` | Payroll content contains sensitive employee information and has a non-standard label. |
| `S-016` | Audit and Review Findings | Confidential | `28` | Audit content contains PII and should be validated before Copilot inclusion. |
| `S-017` | Leadership Briefing Notes | Internal | `14` | Internal leadership notes contain PII and may require a stronger label. |
| `S-020` | Personnel Reorg Planning | Confidential | `60` | Personnel planning content contains sensitive employee information. |
| `S-021` | Expense Claims Archive | Internal | `640` | Internal finance archive contains significant PII and may require a stronger label. |
| `S-022` | Old Records (pre-2015) | Blank or missing | `3300` | Highest mapped PII count, missing label, stale content, and anonymous links make this a priority review site. |
| `S-024` | Incident Response Active | Restricted | `9` | Restricted security incident content contains PII and should remain limited to need-to-know access. |

## Over-shared content view

| Site ID | Site name | Anonymous links | External guests | Current label | Handling |
|---|---|---:|---:|---|---|
| `S-002` | ITD Project Plans | No | `2` | Internal | Review guest access and confirm business owner approval. |
| `S-003` | HR Benefits Enrolment | No | `1` | Confidential / All Employees | Review guest access, label protection, and business owner approval. |
| `S-005` | Hansard Broadcast Ops | Yes | `4` | Internal | Remove or justify anonymous links and review guest access. |
| `S-006` | Legal Opinions Library | Yes | `3` | Restricted | Remove anonymous links, review guest access, and confirm business owner approval. |
| `S-008` | Vendor Contracts (active) | No | `6` | Confidential / Anyone (not protected) | Review guest access and correct label protection. |
| `S-010` | Committee Closed Sessions | No | `1` | Restricted | Review guest access and confirm need-to-know approval. |
| `S-011` | General Staff Share | Yes | `11` | Internal | Remove or justify anonymous links and review broad guest access. |
| `S-012` | Constituency Office Files | No | `2` | Confidential / Trusted People | Review guest access and confirm business owner approval. |
| `S-013` | ITD Project Plans | No | `2` | Internal | Possible duplicate of `S-002`; confirm correct record and review guest access. |
| `S-018` | Training Materials | No | `1` | Internal | Review guest access and confirm business owner approval. |
| `S-019` | Network Diagrams and Plans | Yes | `0` | Internal | Remove or justify anonymous links before go-live. |
| `S-022` | Old Records (pre-2015) | Yes | `0` | Blank or missing | Remove anonymous links and correct missing label before go-live. |

## Data issues found

### site_inventory.csv

| Issue | Site ID(s) | Correction / handling |
|---|---|---|
| Inconsistent date formats | `S-001` to `S-024`, mixed formats across the file | Standardize `last_modified` to `MM/DD/YYYY` using Excel date format and manual correction. |
| Non-lowercase emails | `S-001`, `S-013`, `S-023` | Convert owner emails to lowercase. |
| Possible duplicate | `S-002`, `S-013` | These rows have very similar data and only the item count differs. No correction applied. To be reviewed with the owner. |
| Email with trailing space | `S-013` | Remove trailing space from `Carlo.Munoz@leg.bc.ca `. |
| Garbled text / encoding issue | `S-005` | `Hansard â€" Broadcast Ops` has garbled text. Remove the garbled character. |
| Non-site summary row | `TOTAL (as reported by ITD admin)` | Exclude from site-level analysis and label coverage counts. |
| Summary total | `TOTAL (as reported by ITD admin)` | The total in the summary row, `196900`, does not match the sum of the item counts, `157174`. To be reviewed with ITD Admin. |
| Missing external guest details in sharing links file | `S-002`, `S-003`, `S-005`, `S-006`, `S-008`, `S-010`, `S-011`, `S-012`, `S-013`, `S-018` have an external guest count that does not match the count of entries in the sharing links file. | Investigation into external sharing needs to be conducted. |

### sharing_links.csv

| Issue | Site ID(s) | Correction / handling |
|---|---|---|
| Anonymous `link_type` discrepancy | `S-006` has an entry with anonymous type but explicit target, which does not match other entries. | No correction applied. To be reviewed with the owner to confirm whether this is correctly configured. |
| Specific `link_type` discrepancy | `S-012` has an entry with specific type but no explicit target, which does not match other entries. | No correction applied. To be reviewed with the owner to confirm whether this is correctly configured. |

### pii_detections.csv

| Issue | Site ID(s) | Correction / handling |
|---|---|---|
| `site_id` discrepancy | `S-099` and `S-101` are not found in other files. | No correction applied. Investigation of the source of these entries should be conducted. |
| Duplicate Scan | `S-003` has a listed duplicate scan. | The duplicate entry was removed. Investigation of the source of these entries should be conducted. |

## Claims to verify

- **All 900 staff are licensed and Copilot-eligible.**  
  This is not supported by the provided licensing file. The file shows some users without E7 licences, and the total user count is much lower than 900.

- **The early read of the scan suggests 847 files contain Social Insurance Numbers.**  
  The PII file contains numeric SIN match counts, but the 847-files claim is not confirmed. Numeric SIN rows total 448 in pii_detections file. The unmapped S-099 row also lists SIN as “many,” so the result should be validated before reporting a confirmed file count.

- **The classifications follow the Assembly’s standard and confirm FOIPPA compliance.**  
  The classifications are based on the provided classification standard and should be treated as guidance only. They do not confirm FOIPPA compliance. FOIPPA compliance must still be assessed separately based on collection, use, disclosure, access controls, retention, residency, and business context.
 