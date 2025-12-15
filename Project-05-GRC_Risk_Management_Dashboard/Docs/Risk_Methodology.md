# Risk Methodology

## Purpose
This document outlines the methodology used to identify, assess, and score risks
presented in the Risk Management Dashboard.

The objective is to ensure **consistency, transparency, and auditability** in how
risk ratings are derived and represented across the dashboard.

---

## Risk Identification
Risks were identified and grouped based on **risk domains relevant to information
security and operational resilience**, as reflected in the dashboard.

The primary risk categories used in this analysis include:
- Confidentiality
- Access Control
- Availability
- Malware
- Social Engineering

Each risk is defined with a clear description and assigned to **one primary risk
category** to support aggregation and comparative analysis.

---

## Risk Scoring Dimensions
Risk evaluation is based on two core dimensions:

### Likelihood
Likelihood represents the probability that a risk event will occur, given the
current environment and threat landscape.

The dashboard uses a **1–5 scale**, where:
- 1 = Very Low
- 2 = Low
- 3 = Moderate
- 4 = High
- 5 = Very High

---

### Impact
Impact reflects the potential severity if the risk materializes. Impact considers
the effect on:
- Information confidentiality
- System availability
- Operational continuity
- Organizational reputation

The dashboard uses a **1–5 scale**, where:
- 1 = Minimal impact
- 2 = Minor impact
- 3 = Moderate impact
- 4 = Major impact
- 5 = Severe impact

---

## Inherent Risk
Inherent Risk represents the level of risk **before any controls are applied**.

It is calculated using the following formula:

Inherent Risk = Likelihood × Impact

This score represents the organization’s **baseline risk exposure** for each risk
category and individual risk.

---

## Residual Risk
Residual Risk represents the remaining level of risk **after controls or mitigations
are considered**.

Where applicable, control effectiveness is evaluated and reflected in adjusted
risk values within the dashboard to illustrate risk reduction.

---

## Risk Aggregation and Categorization
Risk values are aggregated at the **risk category level** to support comparative
analysis across domains.

The dashboard may also display a **Grand Total** value, representing the combined
risk exposure across all categories, to provide an enterprise-level perspective.

---

## Risk Prioritization
Risk scores are grouped into qualitative tiers:
- Low
- Medium
- High

These tiers support:
- Risk prioritization
- Management review
- Resource allocation decisions

---

## Dashboard Alignment
All metrics, charts, and KPIs in the Risk Management Dashboard directly map to the
methodology described in this document.

This alignment ensures that:
- Visualizations accurately represent underlying risk logic
- Risk scores are defensible and repeatable
- The dashboard can support governance, audit, and executive decision-making
