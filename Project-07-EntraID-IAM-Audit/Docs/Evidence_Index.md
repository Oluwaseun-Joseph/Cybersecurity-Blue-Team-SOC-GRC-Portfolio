# Evidence Index — Project 07: Microsoft Entra ID IAM Audit

This index maps all evidence artifacts (screenshots + exports) to audit steps and findings.
Screenshots are stored under `Evidence/` and data exports under `Files/`.

---

## Screenshots — Before State

| Figure | File Path | What It Shows | Why It Matters |
|---|---|---|---|
| Figure 1 | Evidence/Before/Screenshots/Figure1_Tenant_Confirmed.png | Active Azure/Entra tenant confirmed (personal tenant) | Confirms audit scope and tenant ownership |
| Figure 2 | Evidence/Before/Screenshots/Figure2_ResourceGroup_Created.png | Resource group created for lab setup | Establishes controlled lab environment context |
| Figure 3 | Evidence/Before/Screenshots/Figure3_ResourceGroup_Details.png | Resource group configuration/details | Supports environment documentation and reproducibility |
| Figure 4 | Evidence/Before/Screenshots/Figure4_BreakGlass_GlobalAdmin_Assigned.png | Break-glass account assigned Global Administrator | Validates emergency admin access control design |
| Figure 5 | Evidence/Before/Screenshots/Figure5_GlobalAdmins_Review.png | Review showing two Global Administrators | Evidence for privileged access exposure finding |
| Figure 6 | Evidence/Before/Screenshots/Figure6_Test_Users_Created.png | Test workforce users created (admin/dev/helpdesk/security analyst) | Shows role-based user population for audit |
| Figure 7 | Evidence/Before/Screenshots/Figure7_Security_Groups_Created.png | Security groups created for RBAC simulation | Demonstrates RBAC intent (group-driven access design) |
| Figure 8 | Evidence/Before/Screenshots/Figure8_Baseline_Group_Memberships_Before.png | Baseline group memberships (before state) | Establishes “before” state for access review |

---

## Screenshots — After State / Observed Limitation

| Figure | File Path | What It Shows | Why It Matters |
|---|---|---|---|
| Figure 9 | Evidence/After/Screenshots/Figure9_EntraID_Free_No_GroupRoleAssignment.png | Entra ID Free does not expose group-based role assignment controls | Documents governance/licensing constraint impacting RBAC enforcement |

---

## Data Exports

| Artifact | File Path | Description |
|---|---|---|
| CSV Export | Files/GlobalAdmin_Assignments.csv | Exported Global Administrator role assignments (primary evidence for privileged role state) |

---

## Notes
- Evidence is intentionally stored outside the report body for traceability and audit-style documentation.
- Figures referenced in the audit report align 1:1 with file names above.
