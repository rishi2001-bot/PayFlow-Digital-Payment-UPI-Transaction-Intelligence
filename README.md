# PayFlow — Digital Payment & UPI Transaction Intelligence

**Power BI | Power Query | DAX | Data Analysis | Synthetic Data**

PayFlow is an interactive Power BI portfolio project built to demonstrate how digital payment data can be analysed to monitor transaction performance, investigate payment failures, understand customer and merchant patterns, and review operational risk indicators.

> **Data disclaimer:** This project uses synthetic data created for learning and portfolio demonstration. The figures do not represent actual UPI, bank, payment gateway, merchant, or customer performance.

## Business problem

Payment operations generate data across transactions, customers, merchants, banks, gateways, devices, locations, refunds, and operational incidents. Reviewing these datasets separately makes it difficult to develop a consolidated view of payment performance.

PayFlow brings these datasets into a common analytical model and presents key measures through an interactive dashboard. It is designed to help stakeholders explore payment outcomes, identify patterns that may require investigation, and monitor operational exceptions.

## Project objectives

- Monitor transaction volume, transaction value, success rate, and failure rate.
- Identify common transaction failure reasons.
- Compare failure rates across payment gateway types.
- Analyse processing time and hourly transaction activity.
- Explore transaction value by customer segment and merchant category.
- Review customer account status.
- Monitor synthetic risk indicators, reversals, refunds, and operational incidents.
- Demonstrate an end-to-end business intelligence workflow using data preparation, data modelling, DAX, and dashboard design.

## Dashboard overview

The report contains four pages:

| Dashboard page | What it covers |
|---|---|
| **Executive Overview** | Overall transaction volume and value, success and failure rates, risk-flagged transactions, monthly transaction trends, status distribution, and leading merchant categories by transaction value. |
| **Transaction Performance** | Failure reasons, failure rate by gateway type, average processing time by transaction status, and transaction activity by hour. |
| **Customer & Merchant** | Transaction value by customer segment, average transaction value by merchant category, customer account status, and merchant-category performance. |
| **Risk & Exceptions** | Risk-flagged transactions, reversal rate, incident volume and severity, risk types, and incident resolution time. |

## Dataset

The project is built from CSV fact and dimension tables.

**Fact tables**

| Table | Rows | Description |
|---|---:|---|
| `Fact_Transactions` | 100,000 | Transaction records, outcomes, amounts, and processing time |
| `Fact_Refunds` | 6,500 | Refund records and processing details |
| `Fact_Incidents` | 1,500 | Operational incident records and resolution details |

**Dimension tables**

| Table | Approx. rows | Description |
|---|---:|---|
| `Dim_Customer` | 10,000 | Customer attributes and segments |
| `Dim_Merchant` | 2,000 | Merchant attributes and categories |
| `Dim_Bank` | 30 | Bank attributes |
| `Dim_Payment_Gateway` | 10 | Payment gateway attributes |
| `Dim_Location` | 200 | Geographic attributes |
| `Dim_Device` | 10,000 | Device, operating system, and network attributes |
| `Dim_Date` | 730 | Calendar attributes covering 2025–2026 |

See [`PayFlow_Data_Dictionary.xlsx`](PayFlow_Data_Dictionary.xlsx) for the field-level reference.

## Data preparation

The source data included selected quality issues to demonstrate practical data-cleaning steps.

- Removed 75 duplicate transaction rows, leaving 100,000 transaction records.
- Standardised inconsistent `Payment_Method` text values, including variations in spacing and capitalisation.
- Replaced 30 missing `Merchant_Category` values with `Unknown`.
- Replaced 150 missing `App_Version` values with `Unknown`.
- Retained large transaction-amount values rather than automatically deleting potential outliers.

## Data model

The report uses a dimensional model with shared dimensions connected to the transaction, refund, and incident fact tables.

- `Fact_Transactions` is the primary transaction fact table.
- `Fact_Refunds` and `Fact_Incidents` provide supporting operational data.
- Customer, merchant, bank, gateway, device, location, and date dimensions provide descriptive context.
- The intended relationship pattern is one-to-many from dimensions to related fact tables, using single-direction filtering.
- Direct fact-to-fact relationships are avoided.

## Key KPIs

| KPI | Meaning |
|---|---|
| Total Transactions | Count of transaction records |
| Total Transaction Value | Sum of transaction amounts |
| Successful Transactions | Count of transactions with Successful status |
| Failed Transactions | Count of transactions with Failed status |
| Success Rate | Successful transactions divided by total transactions |
| Failure Rate | Failed transactions divided by total transactions |
| Average Transaction Value | Average transaction amount |
| Average Processing Time | Average transaction processing time, in milliseconds |
| Risk-Flagged Transactions | Count of records marked with a risk flag |
| Reversal Rate | Reversed transactions divided by total transactions |
| Total Refund Value | Sum of refund amounts |
| Total Incidents | Count of operational incident records |
| Average Incident Resolution Time | Average incident resolution time, in minutes |

## Current dataset snapshot

The following figures describe the current synthetic dataset and dashboard output only:

- **Total transactions:** 100,000
- **Successful transactions:** 80,690
- **Failed transactions:** 11,245
- **Success rate:** approximately 80.69%
- **Failure rate:** approximately 11.25%
- **Total transaction value:** approximately 676.85M in the dataset's currency units
- **Risk-flagged transactions:** approximately 3K
- **Incident records:** 1,500
- **Average incident resolution time:** approximately 88.05 minutes

These values are not industry benchmarks and should not be interpreted as actual payment-network performance.

## Limitations and considerations

- **Synthetic data:** All records and patterns are generated. They cannot support claims about real UPI or payment-industry performance.
- **Risk flags are not confirmed fraud:** `Risk_Flag` and `Risk_Type` are synthetic investigation indicators, not validated fraud labels.
- **No causal conclusions:** Differences between gateways, statuses, or groups do not establish cause and effect.
- **Counts depend on exposure:** Failure counts and transaction-value totals are not automatically adjusted for differences in transaction volume, customer count, or merchant count.
- **Gateway comparisons need context:** Small differences in failure rates should not be treated as definitive rankings without sample-size and transaction-mix analysis.
- **Transaction value is not revenue:** The total transaction value does not represent company revenue, fees, margin, or profit.
- **Incidents are separate records:** An incident is an operational issue recorded in `Fact_Incidents`; it is not the same as a failed transaction. The data does not imply that every failed transaction creates an incident.
- **No SLA assessment:** Severity labels are present, but the project does not define approved response-time targets or calculate SLA breaches.
- **Refund date coverage:** Refund records extend to 13 January 2027, while `Dim_Date` ends on 31 December 2026. Extend the date table before analysing refund dates beyond 2026.
- **Unknown values remain:** Missing merchant categories and app versions are represented as `Unknown`.
- **Outliers are retained:** Large transaction amounts require business-rule and source validation before they can be classified as errors.
- **Static data:** The dashboard does not provide live transaction monitoring, streaming, or automated alerting.

## Tools and skills

- **Power BI Desktop:** Dashboard development, report interactions, slicers, and navigation
- **Power Query:** Data cleaning, standardisation, merging, and transformation
- **DAX:** KPI measures, calculations, and time-based analysis
- **Data modelling:** Fact tables, dimension tables, and shared dimensions
- **Analytics:** KPI design, segmentation, trend analysis, and performance comparison
- **Business communication:** Translating metrics into operational questions and documenting analytical limitations

## How to use

1. Download or clone this repository.
2. Review the CSV files in the `Data` folder.
3. Refer to `PayFlow_Data_Dictionary.xlsx` to understand the fields.
4. Open `PowerBI/PayFlow_Dashboard.pbix` in Power BI Desktop.
5. If Power BI prompts for missing source files, update the file paths to the CSV files in the repository's `Data` folder.

The Power BI report file should be included in the `PowerBI` folder for the dashboard to be directly inspectable. If that file is not present in the repository copy you downloaded, the CSV data and data dictionary alone are not the interactive dashboard.

## Disclaimer

PayFlow is an independent educational portfolio project. It is not affiliated with, endorsed by, or representative of any real payment network, bank, payment gateway, merchant, or company. All names and data are fictional or synthetic. The dashboard is not intended for financial, operational, regulatory, or fraud-related decision-making.
