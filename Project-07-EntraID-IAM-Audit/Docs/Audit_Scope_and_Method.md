# Audit Scope and Methodology

## Objective
Define the purpose of the IAM audit and the security risks being evaluated.

## Scope
- Microsoft Entra ID tenant (lab environment)
- User accounts, groups, and directory roles
- Privileged access assignments
- Break-glass account configuration

## Out of Scope
- Azure resource RBAC
- External identity providers
- Conditional Access and PIM (not available in Entra ID Free)

## Methodology
- Manual role and access review
- Group and user membership analysis
- Privileged role inspection
- Evidence collection via portal screenshots and CSV exports

## Assumptions
- Tenant operates under Microsoft Entra ID Free licensing
- No production workloads are hosted
- Misconfigurations are intentionally introduced for audit demonstration

## Limitations
- Group-based privileged role assignment not supported
- Privileged Identity Management unavailable
