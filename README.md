
# SharePoint Policy Document Control & Signing Workflow

## Overview
This repository documents a governed SharePoint Online and Power Automate workflow designed to manage **policy documents** from draft through approval and signature, ensuring that finalized policies are **locked, read-only, and preserved as PDFs** for compliance and audit purposes.

The workflow enforces clear **separation of duties** between authors, editors, reviewers, and signers, and ensures that once a policy is signed, it cannot be altered.

---

## Business Requirement
- Allow **authors and editors** to collaboratively draft policy documents.
- Route documents through a **formal review and approval process**.
- Capture **electronic signatures** for approved policies.
- Automatically convert signed documents to **read-only PDF format**.
- Preserve an **audit trail** and apply retention policies.
- Prevent any edits after final approval and signature.

---

## Roles & Responsibilities

| Role | Permissions |
|----|----|
| Authors | Create and edit drafts |
| Editors | Edit and format content |
| Reviewers | Read and approve |
| Signers | Sign approved documents |
| Compliance / Admins | Full control |
| General Staff | Read-only (final PDFs) |

---

## End-to-End Workflow

### 1️⃣ Draft Phase
**Library:** `Policy Drafts`

- Authors and editors collaborate on Word documents.
- Versioning enabled (major & minor).
- Metadata captured:
  - Document Status = `Draft`
  - Policy Owner
  - Review Cycle
  - Department

**Permissions:**
- Authors / Editors → Edit
- Reviewers → Read
- Others → No access

---

### 2️⃣ Review & Approval Phase
**Trigger:** Author submits document for review.

**Power Automate Actions:**
- Sequential or parallel approval process.
- Reviewers can approve or request changes.
- If changes are requested, document returns to Draft phase.

**On Approval:**
- Document Status updated to `Approved – Pending Signature`

---

### 3️⃣ Signing Phase
**Trigger:** All reviewers approve.

**Actions:**
- Route document for electronic signature (Adobe Sign / DocuSign / M365 Approvals).
- Capture:
  - Signer name
  - Date signed
  - Approval record

---

### 4️⃣ Finalization (Post-Signature Controls)
Once signed, the system automatically:

- Converts the document to **PDF**
- Stores the PDF in **Policy Final Library**
- Applies **read-only permissions**
- Locks metadata fields
- Retains the original Word document with restricted access

**Final Library Permissions:**
- All Staff → Read
- Authors / Editors → Read-only
- Compliance / Admins → Full Control

---

### 5️⃣ Governance & Compliance
- Retention labels applied (example: 7 years).
- Audit history preserved:
  - Draft versions
  - Approval records
  - Signature confirmation
- Searchable metadata enabled.
- No post-signature modification allowed.

---

## Key Impacts
- Ensured **content integrity** for official policies.
- Eliminated risk of post-approval document changes.
- Improved audit readiness and regulatory compliance.
- Standardized policy lifecycle management across departments.

---

## Screenshots & Diagrams
Screenshots and diagrams illustrating the workflow, permissions, and automation logic are available in the 
![ Policy Document Control & Signing Workflow](Reservation-Dashboard.jpg)`photo_2026-01-07_12-55-32.jpg` folder.

> All images are redacted to remove confidential information.

---

## Repository Structure
