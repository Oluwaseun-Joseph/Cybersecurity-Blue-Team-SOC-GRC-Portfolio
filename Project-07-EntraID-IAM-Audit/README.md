# Project 07 — Microsoft Entra ID IAM Audit (Privileged Access Review)

## Why this project matters
This project demonstrates how an IAM/GRC analyst performs a **privileged access review** in Microsoft Entra ID:
- verifies administrative role assignments,
- validates a break-glass account,
- designs RBAC using groups,
- exports role assignment evidence,
- and documents governance constraints as formal audit findings.

This mirrors real environments where security controls may be limited by **licensing or tenant configuration**, requiring **evidence-backed risk documentation** and compensating controls.

---

## What I did (high-level)
- Confirmed audit scope in a personal Entra ID tenant (Figure 1)
- Created a controlled lab environment (Figures 2–3)
- Verified break-glass administrative access (Figure 4)
- Reviewed Global Administrator exposure (Figure 5 + CSV export)
- Created workforce test users and RBAC groups (Figures 6–8)
- Attempted group-based directory role assignment and documented Entra ID Free limitation (Figure 9)
- Produced an audit-style report with evidence references and an evidence index

---

## Key finding (industry-realistic)
**Group-based directory role assignment was not available** due to Microsoft Entra ID Free licensing.
Instead of fabricating results, the project documents:
- observed limitation (Figure 9),
- risk impact (privilege sprawl risk),
- and remediation (upgrade to Entra ID P1/P2 + compensating controls).

---

## Files included
- `Files/GlobalAdmin_Assignments.csv` — primary evidence export of Global Administrator assignments
- `Files/IAM_Audit_Report.pdf` — final audit report (you can generate from the included content)
- `Docs/Evidence_Index.md` — maps every figure to file paths
- `Evidence/` — before/after screenshots supporting the audit trail

---

## Evidence map
See: `Docs/Evidence_Index.md`

---

## Skills demonstrated
- IAM auditing and privileged access review
- Microsoft Entra ID administration
- Role assignment evidence export and traceability
- RBAC design (groups + membership baselining)
- Audit-style findings and remediation writing
- Governance awareness (licensing constraints + compensating controls)

---

## Notes for reviewers
This project intentionally follows an enterprise audit approach:
- The report references evidence by figure number.
- Screenshots and exports are stored separately for traceability.

## Repository Structure
'''
- Project-07-EntraID-IAM-Audit/
├── Docs/
├── Evidence/
│   ├── Before/
│   │   └── Screenshots/
│   └── After/
│       └── Screenshots/
└── Files/
'''
