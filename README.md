# SAP S/4HANA FI-MM Procure-to-Pay Learning Portfolio

A structured SAP S/4HANA FI-MM learning portfolio that translates Procure-to-Pay (P2P) business requirements into process design, accounting logic, configuration rationale, master data, invoice controls, functional test design, exception analysis, and user documentation.

---

## Project Overview

This repository documents my independent learning of SAP S/4HANA Finance (FI) and Materials Management (MM), with a specific focus on the end-to-end Procure-to-Pay process and FI-MM integration.

The project follows this functional lifecycle:

```text
Business Requirement
        ↓
SAP P2P Process Design
        ↓
FI-MM Accounting Impact
        ↓
Configuration Rationale
        ↓
Master Data
        ↓
Three-Way Match and Invoice Verification
        ↓
Functional Test Design
        ↓
Exception Analysis
        ↓
Illustrative Defect Management
        ↓
User Documentation
```

---

## Project Boundary

This is an independent learning project created using synthetic business data.

The repository demonstrates my understanding of SAP S/4HANA FI/MM business processes, integration concepts, functional design, and testing methodology.

It does **not** represent:

- A customer implementation
- Production-system configuration
- Employer project work
- Live SAP transaction execution
- Completed SIT or UAT in an SAP environment
- SAP implementation experience

Configuration content represents conceptual functional design and configuration rationale unless explicitly stated otherwise. Functional test cases are designed scenarios and are not presented as transactions executed in a live SAP system.

---

## SAP Scope

The portfolio is aligned to concepts relevant to **SAP S/4HANA Cloud Private Edition**.

Primary functional areas covered:

- SAP Financial Accounting (FI)
- SAP Materials Management (MM)
- Procure-to-Pay (P2P)
- Accounts Payable
- FI-MM Integration
- Supplier / Business Partner concepts
- Material Master
- Purchase Requisition and Purchase Order
- Goods Receipt and Invoice Verification
- Three-Way Match and GR/IR Clearing
- Automatic Account Determination concepts
- Invoice Exceptions
- Supplier Liability, Payment, and Clearing
- Functional Testing and Defect Management concepts

---

## Business Scenarios

### Primary Scenario: Nova Manufacturing

The main end-to-end scenario is based on a fictional manufacturing organization called **Nova Manufacturing**.

| Object | Synthetic Value |
|---|---|
| Company Code | NM01 |
| Plant | PL01 |
| Purchasing Organization | NP01 |
| Purchasing Group | PG01 |
| Storage Location | SL01 |
| Supplier | V10001 |
| Material | RM-1001 |

Example procurement: **100 units × INR 500 = INR 50,000**.

This scenario demonstrates business requirements, P2P flow, FI-MM accounting, enterprise structure, configuration rationale, master data, and three-way matching.

### Secondary Scenario: IT Equipment Procurement

A second synthetic scenario is used for functional testing, invoice exceptions, illustrative defect-management examples, and user documentation.

| Object | Synthetic Value |
|---|---|
| Company Code | SM01 |
| Plant | BLR1 |
| Purchasing Organization | IN01 |
| Purchasing Group | P01 |
| Storage Location | RM01 |
| Supplier | SUP1001 |
| Material | LAPTOP-001 |

Example procurement: **10 laptops × INR 50,000 = INR 500,000**.

An illustrative PO value above INR 500,000 may be used in workflow testing to demonstrate an additional approval condition. This secondary scenario should not be interpreted as a separate real implementation.

---

## End-to-End P2P Process

```text
Business Requirement
        ↓
Purchase Requisition
        ↓
Source Determination
        ↓
Purchase Order and Approval
        ↓
Goods Receipt
        ↓
Supplier Invoice
        ↓
Invoice Verification
(PO ↔ Goods Receipt ↔ Invoice)
        ↓
Invoice Posting / Payment Block
        ↓
Payment and Clearing
```

The exact process may vary depending on material, service, account assignment, organizational design, and system configuration.

---

## Key FI-MM Accounting Flow

The following entries are simplified learning examples.

### Purchase Order

Normally, no FI accounting document is generated when a standard purchase order is created.

### Goods Receipt – Stock Material

```text
Dr Inventory
    Cr GR/IR Clearing
```

### Goods Receipt – Consumable / Account-Assigned Purchase

```text
Dr Expense / Consumption
    Cr GR/IR Clearing
```

### Supplier Invoice

```text
Dr GR/IR Clearing
Dr Recoverable Input Tax, where applicable
    Cr Supplier
```

### Supplier Payment

```text
Dr Supplier
    Cr Bank
```

Actual postings depend on material valuation, account assignment, tax treatment, price control, movement type, invoice variance, and automatic account determination.

---

## Repository Navigation

| Section | Purpose |
|---|---|
| [01 – Business Requirements](./01-business-requirements/) | Primary scenario, requirements, assumptions, and terminology |
| [02 – Process Flows](./02-process-flows/) | End-to-end P2P process and responsibilities |
| [03 – Accounting Entries](./03-accounting-entries/) | FI-MM postings, GR/IR, liability, payment, and reconciliation |
| [04 – Configuration Rationale](./04-configuration-rationale/) | Business rationale for FI and MM design decisions |
| [05 – Master Data Templates](./05-master-data-templates/) | Synthetic supplier and material templates with quality checks |
| [06 – Three-Way Match](./06-three-way-match/) | Exact match, variance, missing receipt, and invoice controls |
| [07 – Functional Test Design](./07-test-scripts/) | Positive, negative, boundary, reversal, and integration scenarios |
| [08 – Invoice Exception Analysis](./08-exception-analysis/) | Root cause, corrective action, preventive action, and ownership |
| [09 – Illustrative Defect Management](./09-defect-log/) | Simulated defects, prioritization, resolution, and retest concepts |
| [10 – Functional User Guide](./10-user-manual/) | Conceptual P2P user procedures and troubleshooting |
| [11 – Project Presentation](./11-project-presentation/) | Recruiter-friendly portfolio overview |

---

## Portfolio Highlights

This project demonstrates my developing ability to connect:

**Business Requirement → SAP Process → Configuration Rationale → Transaction Logic → Accounting Impact → Controls → Test Design**

Key strengths demonstrated:

- End-to-end P2P understanding
- Accounts Payable process knowledge
- FI-MM integration and GR/IR concepts
- Three-way matching and invoice exception analysis
- Functional requirement and process documentation
- Master-data and configuration-rationale thinking
- Functional testing methodology
- Structured user documentation

---

## Start Here – Hiring Managers and Recruiters

For a quick review:

1. [Business Context](./01-business-requirements/)
2. [FI-MM Integration](./03-accounting-entries/)
3. [Functional Design](./04-configuration-rationale/)
4. [Invoice Controls](./06-three-way-match/)
5. [Testing Methodology](./07-test-scripts/)
6. [Problem Analysis](./08-exception-analysis/)
7. [Executive Overview](./11-project-presentation/)

---

## Limitations

I use this portfolio to apply SAP functional concepts through synthetic scenarios rather than claim experience from a customer SAP implementation.

- No production SAP data is used.
- No customer configuration is reproduced.
- No employer procedures are included.
- No real supplier, invoice, PO, bank, tax, or employee information is included.
- Test cases are design artifacts unless explicitly identified as executed.
- Illustrative defect outcomes do not represent completed SIT or UAT.

---

## Disclaimer

All company names, organizational structures, supplier information, material data, purchase orders, invoices, financial values, test cases, and defect examples used in this repository are synthetic and created solely for learning purposes.

This repository does not contain confidential information from any current or previous employer.

SAP and SAP S/4HANA are trademarks of SAP SE. This is an independent learning portfolio and is not affiliated with or endorsed by SAP SE or any employer.

---

## Author

**Sampath G R**

Accounts Payable professional developing SAP S/4HANA FI/MM functional knowledge with a focus on Procure-to-Pay and FI-MM integration.

GitHub: [SampathGR-SAP](https://github.com/SampathGR-SAP)
