# 03 — App Flow Document

## Document control
- Product: Karolens
- Version: 1.0-draft
- Date: 2026-11-07

## 1. Navigation model
Main navigation: Dashboard, Customers, Projects, Planning & Materials, Engineering, Compliance, Quality, Billing, Reports, Documents/Knowledge, Settings. Role-based visibility is convenience only; backend authorization is authoritative.

## 2. First-time organization setup
1. Sign up / accept invitation.
2. Create organization profile: business name, address, business profile, contacts, timezone and logo.
3. Invite members and assign tenant-scoped roles.
4. Configure project numbering, IDR currency, document categories, approval matrix and notification preferences.
5. Configure company compliance profile and applicability owner.
6. Dashboard empty state guides first project.

## 3. Customer-to-project flow
1. Create customer/contact.
2. Create quotation/opportunity with vehicle/body type, quantity, high-level requirements and target delivery.
3. Upload request documents/drawings/contract draft.
4. Create project after order acceptance; link quote/order reference and owner.
5. Create vehicle/unit records (VIN/chassis/engine identifiers only where relevant and authorized).
6. Link contract, obligations, payment milestones and acceptance criteria.

## 4. Document knowledge flow
1. Authorized user uploads file into project workspace.
2. Validate type/size and store immutable original version.
3. Create processing job and show Uploaded/Queued state.
4. Extraction returns candidate text/tables/facts, confidence and citations (document/version/page/region when available).
5. User reviews extracted facts; accepts, edits or rejects each candidate.
6. Approved technical facts become baseline only through authorized action.
7. New file version enters comparison; show detected changes and affected specs/BOM/cost/schedule/obligations.
8. Change request requires impact assessment and approval before baseline update.

## 5. Project execution overview
Overview shows customer, contract amount (role restricted), units, lifecycle status, approved spec revision, delivery forecast, next milestone, blockers, material readiness, production progress, compliance/QC release status, invoice/receivable status and recent activity.

Project tabs: Overview; Requirements & Drawings; Contract & Changes; BOM & Materials; Schedule & Production; Compliance; Quality; Customer Reports; Billing; Delivery & Warranty; Documents; Audit History.

## 6. Engineering and BOM flow
1. Draft spec/configuration from customer requirements and approved drawings.
2. Engineer reviews mandatory fields/conflicts.
3. Approve spec revision baseline.
4. Create BOM revision linked to approved specification.
5. Calculate required materials/components; compare stock/reservations/open purchase orders.
6. Generate shortage list and purchase request.
7. Spec revision triggers impact preview: BOM deltas, cost delta, material availability, schedule and compliance impact.
8. Authorized approval creates new baseline; preserve prior revision.

## 7. Procurement and production flow
1. PPIC creates schedule with operations, dependencies, resources and planned dates.
2. Procurement converts shortages to RFQ/PO (MVP may use internal purchase request + manual PO upload).
3. Warehouse records receipt, inspection, lot/quantity and allocation to project/unit.
4. Production records progress, logs, photos and blockers.
5. Delay event recalculates forecast with cause/confidence; manager confirms customer-facing impact.
6. Rework/nonconformity creates corrective action and affected operation.

## 8. Compliance flow
1. Create applicability profile by company, vehicle category, body type, OEM and location.
2. Generate requirement register from versioned rule library and manually confirmed applicability.
3. Attach evidence to requirement and vehicle/unit.
4. Compliance owner reviews completeness and effective/expiry dates.
5. Track SKRB/SUT/physical inspection/BAP/SRUT external status, reference numbers, fees/due dates and supporting evidence as relevant.
6. Release gate requires applicable mandatory evidence; exception only by authorized role with reason and where lawful. AI extraction alone cannot mark approval complete.

## 9. QC and release flow
1. Select inspection checklist (vehicle/body/OEM/customer/internal SOP).
2. Inspector records result, measurement, photo and evidence.
3. Failed item creates nonconformity/rework.
4. Reinspection closes or escalates issue.
5. Release readiness evaluates contract acceptance, technical checks, mandatory evidence, QC and dossier completeness.
6. Authorized release approval records signatory, time and dossier version.

## 10. Customer reporting and approval
1. Select template and reporting period.
2. Assemble verified progress, milestones, blockers, forecast, approved photos and permitted links.
3. Preview/redact internal costs, margin, suppliers and private notes.
4. Authorized approver edits/approves.
5. Send/download/share via approved channel; log delivery event.
6. Customer response/clarification creates communication record/task.

## 11. Billing and collection
1. Approved contract milestone becomes due on agreed trigger.
2. Finance reviews trigger and creates commercial invoice.
3. Invoice has number/date/due date/items/amount/tax metadata and milestone reference.
4. Record payment and allocate to invoice(s).
5. Recalculate balance; attach proof of payment.
6. Reminder sends through approved channel and logs outcome.
7. Credit/adjustments use permissioned workflow and audit record.

## 12. Delivery and warranty
1. Prepare handover checklist/dossier per unit.
2. Confirm customer acceptance and outstanding conditions.
3. Record delivery date, documents, photos, recipient and condition evidence.
4. Create warranty coverage from approved contract terms and start trigger.
5. Warranty claim creates case, evidence, assessment, disposition, repair tasks and closure.

## 13. Customer portal (later phase)
Customer user sees only explicitly shared projects, approved reports/documents, selected progress/forecast, questions/change approvals, invoices/outstanding and warranty cases. Sharing is scoped, expiring and revocable.

## 14. Global states
Each workflow includes loading, empty, success, validation error, permission denied, conflict/stale version, processing, retryable failure, terminal failure, and queued/offline action where supported. Do not show success before backend confirmation.
