# Project 07 – Microsoft Entra ID IAM Audit

## Overview
This project documents a hands-on **Identity and Access Management (IAM) audit**
conducted in a Microsoft Entra ID tenant to evaluate **privileged access controls,
role assignments, and governance limitations**.

The audit focuses on:
- Global Administrator exposure
- Break-glass account validation
- Role-based access via security groups
- Identification of Entra ID Free licensing constraints

The project mirrors how IAM and GRC teams perform **access reviews, risk identification,
and evidence-backed reporting** in real enterprise environments.

---

## Audit Objectives
- Validate Global Administrator assignments
- Review privileged account exposure
- Assess role-based access control (RBAC) design
- Identify governance and licensing limitations
- Document risks and remediation recommendations

---

## Environment
- Identity Platform: Microsoft Entra ID
- Tenant Type: Entra ID Free
- Users: Admin, Developer, Helpdesk, Security Analyst
- Groups: Cloud-Admins, IT-Helpdesk

---

## Key Findings (High-Level)
- Multiple Global Administrators identified
- Break-glass account properly configured
- RBAC intent designed using security groups
- **Group-based role assignment unavailable due to Entra ID Free licensing**
- Governance limitation documented with evidence

---

## Evidence
All screenshots and exports are indexed in:
📄 `Docs/Evidence_Index.md`

---

## Outcome
Although role assignment to groups could not be enforced due to licensing,
the audit successfully:
- Identified privilege risks
- Documented governance gaps
- Produced defensible audit evidence
- Provided remediation guidance aligned with best practices

---

## Skills Demonstrated
- IAM auditing
- Privileged access review
- Microsoft Entra ID administration
- Risk documentation
- Evidence-based reporting
- GRC-aligned analysis

