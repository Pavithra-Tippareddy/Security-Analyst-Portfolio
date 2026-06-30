# Identity Lifecycle Management — SecureNest HR Solutions

## Project Overview

Designed and implemented a full Identity Lifecycle Management (ILM) framework for **SecureNest HR Solutions**, a fictional 60-person HR consulting firm handling sensitive employee data across client organizations.

This project extends beyond static access control (see [FinBridge IAM project](../IAM-Access-Control-FinBridge)) to demonstrate the **full identity lifecycle** — Joiner, Mover, Leaver (JML) — combined with attribute-based group design, B2B guest identity governance, and least-privilege role delegation, all implemented in a live **Microsoft Entra ID (Free Tier)** tenant.

---

## Deliverables

| File | Description |
|---|---|
| [SecureNest_IAM_Report.docx](./SecureNest_IAM_Report.docx) | Full report — lifecycle framework, group design, risk findings, interview answer guides |
| [Identity Lifecycle Register (Google Sheets)](https://docs.google.com/spreadsheets/d/1oOgxyqzf51pQSUcK75dKfEOTNERpKlayJCogbsuCgw8/edit?usp=sharing) | User inventory, lifecycle events log, group design reference |
| [screenshots/](./screenshots/) | 14 Entra ID portal screenshots — user provisioning, group design, role delegation, B2B guest onboarding, full JML simulation, audit log |

---

## What This Project Demonstrates

| Capability | Evidence |
|---|---|
| Identity lifecycle management (Joiner/Mover/Leaver) | Full simulation on Frank Miller — onboarded, promoted, offboarded with audit trail |
| Attribute-based access design | Job Title, Department, and Company Name used to define group logic |
| Dynamic group design (documented) | 3 dynamic group rules designed and documented — simulated manually due to free-tier licensing limits |
| B2B external identity governance | Guest invitation, time-bound access design, dedicated external auditor group |
| Least-privilege role delegation | Scoped admin roles (Helpdesk Administrator, User Administrator) instead of Global Administrator |
| Audit trail and evidence-based offboarding | Full audit log capturing account lifecycle from creation to disablement |

---

## User Inventory Summary

| Name | Role | Department | Group | Status | Directory Role |
|---|---|---|---|---|---|
| SN-Alice Johnson | HR Consultant | HR Operations | SN-HR-Consultants | Active | None |
| SN-Bob Chen | Senior HR Consultant | HR Operations | SN-HR-Consultants | Active | User Administrator |
| SN-Carol White | Payroll Specialist | Finance | SN-Payroll-Access | Active | None |
| SN-David Park | IT Support Specialist | IT | — | Active | Helpdesk Administrator |
| SN-Emma Davis | External HR Auditor | External (Guest) | SN-External-Auditors | Active (Guest) | None |
| SN-Frank Miller | *(offboarded)* | *(cleared)* | *(removed)* | **Disabled** | None |

---

## Joiner / Mover / Leaver Simulation — Frank Miller

| Stage | Action Taken | Evidence |
|---|---|---|
| **Joiner** | Account created with Job Title: HR Consultant, added to SN-HR-Consultants group | `10_joiner_frank_onboarded.png` |
| **Mover** | Promoted to Senior HR Consultant, Department changed to HR Leadership | `11_mover_frank_promoted.png` |
| **Leaver** | Account disabled, sessions revoked, removed from group, job data cleared | `12_leaver_frank_disabled.png`, `13_leaver_frank_removed_from_group.png` |

All lifecycle events confirmed in the Entra ID audit log with timestamps.

---

## Dynamic Group Design (P1 Feature — Documented)

Entra ID Free Tier does not support Dynamic User groups (requires P1 license). All three groups were designed with their intended dynamic membership rule and implemented as Assigned groups to simulate the same outcome manually.

| Group Name | Intended Dynamic Rule (P1) | Purpose |
|---|---|---|
| SN-HR-Consultants | `user.companyName -eq "SecureNest HR Solutions" -and user.department -eq "HR Operations"` | HR systems access |
| SN-Payroll-Access | `user.jobTitle -eq "Payroll Specialist"` | Finance & Payment Gateway access |
| SN-External-Auditors | `user.userType -eq "Guest"` | Read-only audit access |

---

## B2B Guest Identity — External HR Auditor

Simulated inviting an external auditor (Emma Davis) as a B2B guest rather than a standard member account:

- Authenticates with her own external identity — no password management overhead for SecureNest
- Automatically distinguishable via `userType = Guest` attribute
- Scoped to a dedicated `SN-External-Auditors` group with read-only intent
- Same governance tools (Conditional Access, access reviews) apply to guest accounts as members

---

## Least-Privilege Role Delegation

| User | Role Assigned | Why Not Global Administrator |
|---|---|---|
| SN-David Park (IT Support) | Helpdesk Administrator | Can reset passwords and manage sessions for standard users only — cannot modify tenant settings or admin accounts, limiting blast radius if compromised |
| SN-Bob Chen (Senior HR Consultant) | User Administrator | Scoped to user account management for HR operations — not tenant-wide administrative rights |

---

## Entra ID Screenshots

| Screenshot | What it shows |
|---|---|
| 01_securenest_users.png | All 6 SecureNest users provisioned |
| 02_group_hr_consultants.png | SN-HR-Consultants group created |
| 03_group_payroll.png | SN-Payroll-Access group created |
| 04_all_groups.png | All 3 SecureNest groups listed |
| 05_user_attributes_updated.png | User profile with Job Title, Department, Company populated |
| 06_helpdesk_role_david.png | Helpdesk Administrator assigned to David Park |
| 07_useradmin_role_bob.png | User Administrator assigned to Bob Chen |
| 08_b2b_guest_emma.png | Emma Davis shown as Guest user type |
| 09_external_auditors_group.png | Emma added to SN-External-Auditors |
| 10_joiner_frank_onboarded.png | Frank Miller — joiner stage |
| 11_mover_frank_promoted.png | Frank Miller — promotion / mover stage |
| 12_leaver_frank_disabled.png | Frank Miller — account disabled |
| 13_leaver_frank_removed_from_group.png | Frank Miller removed from group |
| 14_audit_log_securenest.png | Full audit trail — account lifecycle evidence |

---

## Framework References

| Standard | Relevance |
|---|---|
| ISO 27001 Annex A.9.2.1 / A.9.2.6 | User registration and de-registration; removal of access rights on role change or exit |
| NIST CSF PR.AC | Identity management and access control |
| GDPR Article 5(1)(f) | Integrity and confidentiality — applies to HR personal data access |

---

## Free Tier Limitations Identified

| Feature | Limitation | Recommendation |
|---|---|---|
| Dynamic Groups | Requires Entra ID P1 — not available on free tier | Upgrade to P1 for automated attribute-based group membership |
| Conditional Access | Cannot enforce MFA per-role or per-risk | Upgrade to P1 |
| Access Reviews | Cannot automate recurring guest access reviews | Upgrade to P2 |

---

## Tools Used

Microsoft Entra ID (Free Tier) · Microsoft Excel / Google Sheets · Microsoft Word / Google Docs · ISO 27001 · NIST CSF · GDPR
