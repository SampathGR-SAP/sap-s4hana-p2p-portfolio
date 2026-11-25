# P2P Defect Management Guide

## Portfolio Boundary

The defects in this folder are illustrative functional scenarios created to demonstrate defect-management methodology.

They were not identified during an actual SAP implementation, SIT, UAT, or production-support engagement.

Any status, root cause, resolution approach, or retest outcome shown is simulated for learning purposes.

## 1. Purpose

This guide explains an illustrative method for recording, assessing, correcting, retesting, and closing simulated defects in the synthetic SAP S/4HANA Procure-to-Pay learning project.

> **Portfolio note:** All defects, users, document numbers, values, configuration findings, and evidence references are synthetic. This project does not represent a live customer implementation or production support activity.

## 2. What Is a Defect?

For this learning portfolio, an illustrative defect exists when a simulated result does not match a documented requirement, conceptual design, expected accounting outcome, or test-case expectation.

```text
Business Requirement
        ↓
Configuration / Master Data
        ↓
Functional Test Case
        ↓
Expected Result vs Simulated Actual Result
        ↓
Illustrative Defect, if they do not match
```

Not every unexpected observation is a configuration defect. The cause may be test data, master data, user action, authorization, display timing, integration, or an incorrect expectation.

## 3. Defect Lifecycle

```text
New / Open
    ↓
Analysis
    ↓
Assigned
    ↓
In Progress
    ↓
Fixed
    ↓
Retest Required
    ↓
Resolved
    ↓
Closed
```

Alternative outcomes include:

- **Rejected:** The result is working as designed or the reported issue cannot be reproduced.
- **Deferred:** The issue is accepted for later resolution because impact is limited or timing does not allow correction.
- **Pending Business Input:** A process owner must clarify the expected behavior.

## 4. Required Defect Information

Every defect should include:

- Unique defect ID
- Related test-case ID
- Process area
- Clear defect title
- Detailed description
- Exact reproduction steps
- Expected result
- Simulated actual result
- Severity and priority
- Illustrative test phase, such as Illustrative SIT Scenario or Illustrative UAT Scenario
- Root-cause category and confirmed cause
- Assigned owner
- Reported and target dates
- Illustrative resolution approach
- Illustrative retest date and outcome
- Expected evidence type

A statement such as “invoice not working” is not sufficient. A useful title is:

> Quantity variance invoice is not blocked when invoice quantity exceeds received quantity.

## 5. Severity and Priority

Severity describes the business or system impact. Priority describes how urgently the defect should be addressed.

| Severity | Definition | P2P example |
|---|---|---|
| Critical | Core process cannot continue or major financial/control exposure exists | Duplicate invoice posts, or GR debits a materially incorrect inventory account |
| High | Important functionality fails with significant operational impact | Workflow, tolerance block, account assignment, or invoice document flow fails |
| Medium | Process works with a workaround or limited impact | Incorrect payment terms default or source is not proposed |
| Low | Minor usability, display, or documentation issue | Data becomes correct after manual refresh |

A Critical defect is normally High priority. However, severity and priority should remain separate fields because deployment timing and available workarounds can influence urgency.

## 6. Root-Cause Categories

### Configuration

Examples:

- Flexible Workflow condition is incorrect.
- Invoice tolerance does not reflect the approved requirement.
- Automatic account determination selects the wrong G/L account.
- Pricing condition is statistical when it should affect value.

### Master data

Examples:

- Supplier payment terms are incorrect.
- Source-list validity has expired.
- Material valuation class is incorrect.
- Cost center is invalid.

### Test data

Examples:

- Test PO does not contain the intended condition.
- Test supplier is not extended to the required organizational level.
- Incorrect material was used during execution.

### Process design

Examples:

- The requirement does not define who may approve a high-value PO.
- Business ownership for missing GR resolution is unclear.

### Authorization

Examples:

- Test user cannot access a required application.
- User can perform an action that should be restricted.

### Integration

Examples:

- Financial document is not generated after a material movement.
- Data is not transferred to a connected process as expected.

### User error

Examples:

- Tester selected the wrong movement type.
- Invoice was posted without the required PO reference.

Root cause should be confirmed through analysis. Do not classify every failed test as “Configuration.”

## 7. Defect Reporting Method

### Step 1: Reproduce the issue

Repeat the test with the same data. Confirm that the result is not a temporary display or refresh issue.

### Step 2: Define expected evidence

Define only synthetic evidence types, such as:

- Test-case ID
- Synthetic PO or invoice number
- Error-message text
- Workflow log reference
- Material or accounting document reference
- Screenshot filename

### Step 3: Compare design and result

Review the business requirement, configuration rationale, master data, and expected test result.

### Step 4: Assess impact

Ask:

- Does the process stop?
- Can an incorrect financial document be posted?
- Is there duplicate-payment or compliance exposure?
- Is there a safe workaround?
- Does the defect affect one scenario or the entire P2P flow?

### Step 5: Assign ownership

| Finding | Typical owner |
|---|---|
| Workflow or PO configuration | MM functional consultant |
| GR/IR or automatic account determination | FI/MM functional consultant |
| Supplier or material data | Master data team |
| Tax behavior | Tax and FI functional team |
| Missing business rule | Process owner / business analyst |
| Access issue | Security / authorization team |
| Test execution mistake | Test analyst |

### Step 6: Describe the illustrative resolution approach

The illustrative resolution approach should say what would change. Avoid vague text such as “issue fixed.”

Better example:

> Updated the workflow start condition so standard POs above INR 500,000 require the additional approval step.

### Step 7: Describe illustrative retesting

Use the original failed scenario. Also test nearby boundary conditions.

For a workflow threshold of INR 500,000, retest:

- INR 499,999
- INR 500,000
- INR 500,001
- INR 550,000

### Step 8: Run regression testing

After a configuration correction, repeat related successful tests to confirm the fix did not create another problem.

## 8. Retesting and Closure Rules

The lifecycle statuses below describe how a real project would operate. In this portfolio they are simulated labels and do not prove completed SAP test execution.

A defect should be marked **Resolved** only when:

- The correction is available in the test environment.
- The original test case has been executed again.
- Simulated actual result matches expected result.
- Relevant accounting or document-flow impact has been checked.
- Retest evidence is recorded.

It should be marked **Closed** when the result is verified and no further action is required.

If retesting fails, return the defect to **Open** or **In Progress** and record the new actual result.

## 9. Example Defect

### Defect

```text
Defect ID: DEF-P2P-003
Test Case: TC-P2P-009
Title: Quantity variance invoice is not blocked
Severity: High
Priority: High
```

### Test data

```text
PO Quantity:       10 EA
GR Quantity:        8 EA
Invoice Quantity:  10 EA
```

### Expected result

The system identifies the quantity variance and applies the configured invoice block.

### Simulated actual result

The invoice posts without the expected payment block.

### Investigation

Check:

- GR-based invoice verification indicator
- Quantity tolerance settings
- PO and GR history
- Invoice block reason
- Whether the correct company code and test data were used

### Illustrative retest

After correction, repeat the same scenario and verify the invoice status, block reason, document history, and payment eligibility.

## 10. Metrics

The `P2P_Defect_Log.xlsx` workbook supports:

- Total defect count
- Open and in-progress defects
- Fixed items awaiting retest
- Resolved and closed defects
- Critical and High-severity defects
- Root-cause distribution
- Retest pass count
- Closure rate

Metrics should be interpreted together. A lower defect count is not automatically better if testing coverage is weak.

## 11. Relationship to Other Portfolio Sections

```text
07-test-scripts/
└── Designed test case supplies the linked scenario

08-exception-analysis/
└── Business and invoice exceptions are classified and analyzed

09-defect-log/
└── Illustrative defects demonstrate assignment, resolution, retest and closure methodology
```

An invoice exception is not automatically a software or configuration defect. For example, a missing GR may be a process-timing issue rather than a system defect.

## 12. Workbook Structure

### `Defect Log`

Contains ten simulated P2P defect scenarios linked to designed functional test cases, with illustrative severity, status, root cause, owner, dates, resolution approach, and retest outcome.

### `Summary`

Provides formula-based counts by status, severity, root cause, and illustrative retest outcome.

### `Severity Guide`

Explains Critical, High, Medium, and Low severity with P2P examples and closure expectations.

## 13. Confidentiality

Do not upload the following to a public GitHub repository:

- Real employer incident details
- Production SAP screenshots
- Real supplier or invoice information
- Employee names, usernames, or email addresses
- Internal system IDs or URLs
- Confidential configuration values
- Customer-specific process documentation

Use only synthetic data and describe the work as portfolio learning, not as real project delivery experience.
