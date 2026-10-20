# CV1 Asset Pack

This folder contains the sample data + expected outputs for the Data + AI Workshop, Clean Version 1.
All files are deterministic and authoritative — every lab references them from here.

## Files

| File | Used in | Purpose |
|---|---|---|
| cv1_salesforce_customers.csv | Lab 0 | Load into Salesforce CV1_Customer__c (4 rows). |
| cv1_databricks_customer_events.csv | Lab 0 | Load into Databricks cv1_workshop.customer_events (4 rows). |
| cv1_databricks_transactions.csv | Lab 0 | Load into Databricks cv1_workshop.transactions (5 rows). |
| cv1_reference_state_country_city.csv | Lab 4 | Reference 360 code-list source. |
| cv1_expected_dq_exceptions.csv | Lab 4 | Ground truth for DQ exception validation (5 expected). |
| cv1_expected_mdm_golden_records.csv | Lab 5 | Ground truth for Golden Record validation (2 expected). |
| cv1_cai_golden_record_payload.json | Lab 6 | Sample CAI process input on MDM publish event. |

## Personas

- **Sarah Jenkins** — hero. 3 Salesforce rows (sf-001 / sf-002 / sf-003) + 1 Databricks web user (WEB-1).
  Carries every intentional defect that drives the workshop's lessons.
- **Diego Martinez** — sanity. 1 Salesforce row (sf-004) + 1 Databricks web user (WEB-2).
  Clean. Exists so MDM has a non-Sarah Golden Record to prove no over-merge.

## Sarah's intentional defects

- Future Last_Purchase_Date 2028-08-20 (sf-001)
- Invalid email "12345@abc" (sf-002)
- Phone format variation across all rows
- Name spelling "Sarah Jenkens" (sf-003)
- Missing phone (sf-003)
- City aliases ATX (sf-002) and AUS (ev-002)
- State spelled out "Texas" (sf-003)
- Country spelled out "USA" (sf-003)
- Negative-amount transaction TXN-10002 (-200.00)
- Future-dated transaction TXN-10004 (2028-01-01)

## Sarah's expected Golden Record (after Lab 5)

- MDM_Customer_ID: MDM-100001
- Full Name: Sarah Jenkins (from sf-001 — most complete + valid email)
- Email: sarah.j@enterprise.com (from sf-001 — invalid one rejected)
- Phone: 5550198 (normalized)
- Address: Austin, TX 78701, US (standardized)
- Loyalty Tier: Gold
- Consent: Opted In
- Last Purchase Date: 2025-08-01 (from sf-003 — sf-001's future date excluded)
- Lifetime Value: 450.50 (TXN-10001 + TXN-10003; TXN-10002 negative + TXN-10004 future excluded)
- Recent Interest: Hiking Jackets
- Source records: sf-001, sf-002, sf-003, WEB-1
