# Label Configuration Proposal

> Map the scanned content to the four labels (Public / Internal / Confidential / Restricted)
> and the eight descriptors. Propose auto-labelling rules and Copilot scoping for go-live.
> Ground each choice in the provided deck.

## Label mapping
| site_id | proposed_label | go-live_scope | Reasoning |
|---|---|---|---|
| S-001 | Public | In Scope | Public communications content with no identified access issues. |
| S-002 | Internal | Out of Scope until validated | External guest access should be validated before go-live. |
| S-003 | Confidential-People | Out of Scope until validated | External guest access should be validated before go-live. |
| S-004 | Restricted-Financial | Out of Scope | Restricted content should be excluded from Copilot scope at go-live. |
| S-005 | Internal | Out of Scope until remediated | External guest access should be validated and anonymous links should be remediated before go-live. |
| S-006 | Restricted-Legal | Out of Scope | Restricted legal content should be excluded from Copilot scope at go-live. Anonymous links and external guest access should also be remediated. |
| S-007 | Confidential-Member Support | Out of Scope until validated | Current label is blank, so the proposed label is provisional and requires owner validation before go-live. |
| S-008 | Confidential-Commercial | Out of Scope until validated | External guest access should be validated before go-live. |
| S-009 | Confidential-Security | Out of Scope until validated | Security runbooks should be excluded from Copilot scope at go-live until validated by the security team. |
| S-010 | Restricted-Proceedings | Out of Scope | Restricted closed-session proceedings should be excluded from Copilot scope at go-live. External guest access should also be validated. |
| S-011 | Internal | Out of Scope until remediated | External guest access should be validated and anonymous links should be remediated before go-live. |
| S-012 | Confidential-Member Support | Out of Scope until validated | External guest access should be validated before go-live. |
| S-013 | Internal | Out of Scope until validated | External guest access should be validated before go-live. Duplicate scan entry should also be reviewed against S-002. |
| S-014 | Confidential-People | Out of Scope until validated | Payroll records are highly sensitive People data, so permissions and audience scope should be validated before Copilot exposure. |
| S-015 | Public | In Scope | Public job postings are approved public-facing recruitment content. |
| S-016 | Confidential-Audit | Out of Scope until validated | Access requirements should be validated with the data owner before go-live. |
| S-017 | Restricted-Proceedings | Out of Scope | Restricted content should be excluded from Copilot scope at go-live. Leadership briefing notes and senior leadership briefings are listed as Restricted examples in the deck. |
| S-018 | Internal | Out of Scope until validated | External guest access should be validated before go-live. |
| S-019 | Confidential-Security | Out of Scope until remediated | Network diagrams are security-sensitive and anonymous links should be remediated before go-live. |
| S-020 | Restricted-People | Out of Scope | Restricted content should be excluded from Copilot scope at go-live. Unannounced reorganization plans are listed as a Restricted example in the deck. |
| S-021 | Confidential-Financial | Out of Scope until validated | Expense claims may contain personal and financial information. Financial records, including expense claims, are listed under the Financial descriptor in the deck, so access should be validated before go-live. |
| S-022 | Confidential-People | Out of Scope until remediated | Legacy archive contains significant personal information, has no current label, is stale, and has anonymous links. Requires owner review, access cleanup, and retention review before Copilot exposure. |
| S-023 | Public | In Scope | Approved media releases are public-facing Assembly content. |
| S-024 | Restricted-Security | Out of Scope | Restricted incident response content should be excluded from Copilot scope at go-live. |

## Auto-Labelling Rules

| Trigger | Proposed label | Proposed descriptor | Action | Rationale |
|---|---|---|---|---|
| Content is approved for external release, published on the Assembly website, an approved media release, a public job posting, published Hansard, or broadcast proceedings already made public. | Public | N/A | Auto-apply only in approved public publishing locations. Otherwise suggest for owner confirmation. | Public content is safe to share with anyone inside or outside the Assembly. |
| Content is routine Assembly business with no sensitive indicators, such as meeting notes, project plans, schedules, internal training material, IT development notes, status reports, or team updates. | Internal | N/A | Apply as the default where no Confidential or Restricted triggers are found. | Internal is the default label for routine work available to Assembly account holders only. |
| SINs, national IDs, employee records, benefits records, payroll records, hiring records, performance reviews, contact lists, names plus emails and addresses, or 10+ PII matches. | Confidential or Restricted | People | Suggest Confidential-People. Escalate to Restricted-People for senior staff compensation, unannounced personnel reorganization plans, or named-person-only access. | Identifiable personal information creates serious harm if exposed and should be limited to the appropriate team, named guests, or named individuals. |
| Committee records, closed-door committee material, draft meeting minutes, in camera references, pre-tabling material, confidential committee updates, leadership briefing notes, or senior leadership briefing content. | Confidential or Restricted | Proceedings | Suggest Confidential-Proceedings for team-limited proceedings material. Suggest Restricted-Proceedings for closed-door, in camera, pre-tabling, or senior leadership-only material. | Proceedings content may involve committee confidentiality, pre-release material, or institutional integrity risk. |
| Legal advice, privileged communications, counsel opinions, dispute files, litigation material, procurement dispute advice, or solicitor-client privilege terms. | Confidential or Restricted | Legal | Suggest Confidential-Legal for legal work shared with a defined team. Suggest Restricted-Legal for privileged or named-individual-only legal material. | Legal material may carry privilege and could cause serious institutional harm if mishandled. |
| Live procurement records, vendor pricing, bid evaluations, proposals, negotiated contracts, RFP responses, vendor scoring, commercial terms, or contract negotiation drafts. | Confidential or Restricted | Commercial | Suggest Confidential-Commercial. Escalate only where the material is named-individual-only or part of a Restricted leadership briefing. | Commercial content can create financial, contractual, procurement, or stakeholder harm if exposed. |
| Budgets, invoices, expense claims, receipts, financial statements, draft financials, payment data, or procurement-card records. | Confidential or Restricted | Financial | Suggest Confidential-Financial for routine protected financial records. Suggest Restricted-Financial for draft budgets or financials limited to named senior leaders. | Financial records may contain sensitive operational, personal, payment, or pre-publication information. |
| Audit reports, compliance reviews, investigation findings, internal reviews, control findings, remediation findings, or review material not yet shared with affected teams. | Confidential or Restricted | Audit | Suggest Confidential-Audit. Escalate to Restricted-Audit where findings are part of a named-person investigation or create serious institutional integrity risk. | Audit and investigation findings should be limited until validated and formally communicated. |
| API keys, secrets, passwords, connection strings, source code secrets, network diagrams, threat assessments, continuity plans, incident reports, vulnerability details, or active incident response material. | Confidential or Restricted | Security | Suggest Confidential-Security. Suggest Restricted-Security for active security incident response or material that would directly help an attacker. | Security content could assist an attack, expose weaknesses, or increase operational risk if leaked. |
| MLA office staffing, MLA travel arrangements, research requests, constituency files, Member Services Portal records, or service requests provided directly to MLAs. | Confidential or Restricted | Member Support | Suggest Confidential-Member Support. Escalate to Restricted-Member Support only where access must be limited to named individuals or the content includes highly sensitive staffing, travel, security, or constituency details. | Member Support content relates to services provided directly to MLAs and may include sensitive operational or personal details. |
### Note: Where more than one trigger applies, use the highest-risk parent label and the descriptor tied to the highest-risk content.

## Copilot and agent scoping
| Label | Copilot go-live scope | Configuration recommendation | Reason |
|---|---|---|---|
| Public | In scope | Allow Copilot indexing and responses. | Public content is approved for anyone and the deck says Copilot can quote it freely. |
| Internal | In scope | Allow Copilot, but only after removing anonymous links and obvious oversharing. | Internal content is available to Assembly accounts and the AI assistant can reference it. |
| Confidential | Conditionally in scope | Allow only where permissions are clean, audience-based, and reviewed. Prioritize trusted sites like HR, Finance, Legal, Procurement, Audit, Security, and Member Support libraries once access has been validated. | Copilot can use Confidential content where the user already has access, and outputs should inherit the Confidential label. |
| Restricted | Out of scope | Exclude from Copilot entirely. Do not allow summarization, search grounding, or generated answers from Restricted content. | The deck explicitly says Restricted content is excluded from Copilot, even for users who can open the file. |

## Sample-document labels
| Document | Label | Descriptor | Reason |
|---|---|---|---|
| leadership_pack_draft.txt | Restricted | Proceedings | Contains closed-door committee material limited to five named leaders matching Restricted and Proceedings examples from the deck. |
| media_release_approved.txt | Public | N/A | Approved for public release and relates to public-facing Assembly business. No descriptor needed as this is no Confidential or Restricted |
| procurement_card_review.txt | Confidential | Audit | Internal review material not yet shared with affected teams containing audit-style findings or assessment details that should remain limited until validated and formally communicated. |
