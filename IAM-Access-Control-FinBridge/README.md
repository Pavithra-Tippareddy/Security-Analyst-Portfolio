# IAM Access Control Design — FinBridge Solutions

## Project Overview

Designed and implemented a full Identity & Access Management (IAM) framework for **FinBridge Solutions**, a fictional 45-person fintech company processing customer payments and handling sensitive financial data.

This project covers the complete IAM lifecycle:
- RBAC access matrix design across 8 roles and 11 systems
- Risk analysis with 4 findings (2 High, 1 Medium, 1 Informational)
- Live implementation in **Microsoft Entra ID (Free Tier)**
- Contractor offboarding simulation with full audit log evidence
- IT Administrator offboarding procedure
- Framework alignment: ISO 27001 Annex A.9 · NIST CSF PR.AC · GDPR Article 5(1)(f)

---

## Deliverables

| File | Description |
|---|---|
| [FinBridge_IAM_Report.docx](./FinBridge_IAM_Report.docx) | Full IAM report — risk findings, offboarding procedure, interview answer guides, framework reference |
| [Access Matrix (Google Sheets)](https://docs.google.com/spreadsheets/d/100oKyzD-KkYHoOb5gDpSKqGh88xFh9NAev-VS0owGyw/edit?usp=sharing) | RBAC matrix — 8 roles × 11 systems with colour-coded access levels and Risk Flags sheet |
| [screenshots/](./screenshots/) | 9 Entra ID portal screenshots — user provisioning, role assignments, group creation, offboarding simulation, audit log |

---

## Access Matrix Summary

| System | IT Admin | Developer | Finance Officer | HR Manager | Customer Support | Security Analyst | C-Suite | Contractor |
|---|---|---|---|---|---|---|---|---|
| Azure Entra ID | Full Access | No Access | No Access | No Access | No Access | Read Only | No Access | No Access |
| M365 Admin | Full Access | No Access | No Access | Read Only | No Access | No Access | No Access | No Access |
| Endpoint Manager | Full Access | No Access | No Access | No Access | No Access | Read Only | No Access | No Access |
| Firewall Console | Full Access | No Access | No Access | No Access | No Access | Read Only | No Access | No Access |
| HR System | Full Access | No Access | No Access | Full Access | No Access | No Access | Read Only | No Access |
| Finance System | Full Access | No Access | Full Access | No Access | No Access | No Access | Read Only | No Access |
| CRM | Full Access | Read Only | No Access | No Access | Full Access | No Access | Read Only | No Access |
| Code Repository | Full Access | Full Access | No Access | No Access | No Access | No Access | No Access | Scoped Access |
| Payment Gateway | Full Access | No Access | Full Access | No Access | No Access | No Access | No Access | No Access |
| Customer Portal | Full Access | Read Only | No Access | No Access | Full Access | No Access | No Access | Scoped Access |
| Internal Wiki | Full Access | Read Only | Read Only | Read Only | Read Only | Read Only | Read Only | No Access |

---

## Risk Findings

| # | Finding | Severity | Key Recommendation |
|---|---|---|---|
| 1 | IT Administrator — Full Access across all 11 systems | 🔴 High | Implement PAM + Just-In-Time access; quarterly privilege review |
| 2 | Developer — No access to Payment Gateway | ℹ️ Info | SoD control confirmed compliant — maintain and verify at every review |
| 3 | C-Suite — Simultaneous access to Finance + HR systems | 🟡 Medium | Enforce MFA on both systems; enable audit logging on all C-Suite sessions |
| 4 | Contractor — No account expiry defined | 🔴 High | Enforce 30-day auto-expiry; assign named account owner; monthly review |

---

## Microsoft Entra ID Implementation

Implemented in a live **Microsoft Entra ID Free Tier** tenant:

**Users created (8):**
Alex Rivera (IT Admin) · Dev User (Developer) · Finance Officer · HR Manager · Support Agent · Security Analyst · CEO FinBridge (C-Suite) · Vendor Contractor

**Security groups created (6):**
- `FinBridge-Privileged-Admins` — Alex Rivera
- `FinBridge-Developers` — Dev User + Vendor Contractor
- `FinBridge-Finance` — Finance Officer + CEO FinBridge
- `FinBridge-HR` — HR Manager
- `FinBridge-CustomerSupport` — Support Agent
- `FinBridge-ReadOnly-Security` — Security Analyst

**Directory roles assigned:**
- Alex Rivera → Global Administrator (mirrors Full Access — Finding 1 evidence)
- Security Analyst → Global Reader (mirrors Read Only — access control evidence)
- HR Manager → User Administrator (scoped identity management)

**Contractor offboarding simulated:**
Vendor Contractor account — disable → revoke sessions → remove from groups → audit log captured

All steps confirmed in Entra ID audit log with timestamps and actor recorded.

---

## Entra ID Screenshots

| Screenshot | What it shows |
|---|---|
| 01_user_provisioning.png | All 9 users listed in Entra ID (8 fictional + admin) |
| 02_alex_global_admin.png | Global Administrator role assigned to Alex Rivera |
| 03_secanalyst_globalreader.png | Global Reader role assigned to Security Analyst |
| 04_hrmanager_useradmin.png | User Administrator role assigned to HR Manager |
| 05_security_groups.png | All 6 security groups listed in Entra ID |
| 06_vendor_account_disabled.png | Vendor Contractor account disabled |
| 07_vendor_sessions_revoked.png | Sessions revoked — StsRefreshToken invalidated |
| 08_vendor_groups_removed.png | Vendor Contractor removed from all groups |
| 09_vendor_audit_log.png | Full audit trail — account lifecycle from provisioning to offboarding |

---

## Framework References

| Standard | Relevance |
|---|---|
| ISO 27001:2022 Annex A.9 | Core access control requirements — least privilege, need-to-know, access reviews |
| ISO 27001 Annex A.9.2.3 | Management of privileged access rights — basis for Finding 1 |
| ISO 27001 Annex A.9.2.6 | Removal of access rights when employment ends — basis for Finding 4 and offboarding procedure |
| ISO 27001 Annex A.9.4.1 | Information access restriction — basis for Finding 3 |
| NIST CSF PR.AC | Identity management and access control — Protect function |
| GDPR Article 5(1)(f) | Integrity and confidentiality of personal data — basis for Finding 3 (HR records) |

---

## Tools Used

Microsoft Entra ID (Free Tier) · Microsoft Excel / Google Sheets · Microsoft Word / Google Docs · ISO 27001:2022 · NIST CSF · GDPR
