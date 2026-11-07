# 03 — App Flow Document

## Document control
- Product: Karolens | Version: 1.0-draft | Date: 2026-11-07

## 1. Navigation model
Main navigation: Dashboard, Customers, Projects, Planning & Materials, Engineering, Compliance, Quality, Billing, Reports, Documents/Knowledge, Settings. Role-based visibility hides inaccessible areas without relying on UI-only security.

## 2. First-time organization setup
1. Sign up / accept invitation.
2. Create organization profile: legal/business name, address, KBLI/business profile, contacts, timezone, logo.
3. Invite members and assign tenant-scoped roles.
4. Configure project numbering, currency (IDR), document categories, approval matrix, notification preferences.
5. Configure company compliance profile and applicability review owner.
6. Setup complete -> dashboard empty state with guided first project.

## 3. Customer-to-project flow
1. Create customer/contact.
2. Create quotation/opportunity with vehicle type/body type, quantities, high-level requirements and target delivery.
3. Upload request documents/drawings/contract draft.
4. Start project after order acceptance; store quote/order reference and project owner.
5. Create vehicle/unit records (VIN/chassis/engine identifiers only where relevant and authorized).
6. Link contract, obligations, payment milestones and acceptance criteria.

## 4. Document knowledge flow
1. Authorized user uploads file into project workspace.
2. Validate type/size and store original immutable version.
3. System creates processing job and displays Uploaded/Queued state.
4. Extraction returns candidate text/tables/facts, confidence and citations (document/version/page/region if available).
5. User reviews extracted facts; accepts, edits or rejects each candidate.
6. Approved technical facts become baseline only through authorized approval action.
7. New document version enters comparison flow; detected changes are displayed side-by-side with affected specs/BOM/cost/schedule/obligations.
8. Change request requires impact assessment and approval before baseline update.

## 5. Project execution overview
Project overview shows: customer, contract amount (role restricted), units, lifecycle status, approved spec revision, delivery forecast, next milestone, blockers, material readiness, production progress, compliance/QC release status, invoice/receivable status and recent activity.

Project tabs: Overview; Requirements & Drawings; Contract & Changes; BOM & Materials; Schedule & Production; Compliance; Quality; Customer Reports; Billing; Delivery & Warranty; Documents; Audit History.

## 6. Engineering and BOM flow
1. Create draft spec/configuration from customer requirements and approved drawings.
2. Engineer reviews mandatory fields and conflicts.
3. Approve spec revision as baseline.
4. Create BOM revision linked to spec revision and vehicle/unit quantity.
5. Calculate required materials/components and compare stock/reservations/open purchase orders.
6. Generate shortage list and purchase request.
7. Revision to spec triggers impact preview: BOM deltas, cost delta, material availability, schedule and regulatory evidence impact.
8. Authorized approval creates new baseline; preserve old one.

## 7. Procurement and production flow
1. PPIC/planner creates project schedule with operations, dependencies, resources and planned dates.
2. Procurement converts shortages to RFQ/PO (initial MVP may use internal purchase request + manual PO upload).
3. Warehouse records receipt, inspection, lot/quantity and allocation to project/unit.
4. Production starts operation and records progress, work logs, photos and blockers.
5. Delay/blocker event recalculates forecast with cause and confidence; manager confirms customer-facing impact.
6. Rework/nonconformity creates corrective action and affected operation.

## 8. Compliance flow
1. Create applicability profile by company, vehicle category, body type, OEM and location.
2. Generate applicable requirement register from versioned rule library and manually confirmed applicability.
3. Attach evidence to requirement and vehicle/unit.
4. Compliance owner reviews completeness and expiry/effective date.
5. For SKRB/SUT/physical type inspection/BAP/SRUT stages, track external status, application/reference numbers, fees/due dates and evidence as relevant; never mark government approval complete based only on AI extraction.
6. Gate release on applicable mandatory evidence; allow documented exception only with authorized role and reason where legally permissible.

## 9. QC and release flow
1. Select applicable inspection checklist (vehicle/body/OEM/customer/internal SOP).
2. Inspector completes result, measurement, photo and evidence.
3. Failed item creates nonconformity/rework.
4. Reinspection closes or escalates issue.
5. Release readiness evaluates contract acceptance, technical checks, mandatory compliance evidence, QC and documentation.
6. Authorized release approval records signatory, timestamp and dossier version.

## 10. Customer reporting and approval
1. Select report template and reporting period.
2. System assembles verified progress, milestone status, blockers, forecast, approved photos and permitted evidence links.
3. Internal preview checks redaction (cost/margin/suppliers/private notes).
4. Project manager/authorized approver edits and approves.
5. Send/download/share through approved channel; delivery event is logged.
6. Customer responses and clarification requests become communication records/tasks.

## 11. Billing and collection
1. Contract milestone becomes due based on approved event/approval.
2. Finance reviews trigger and creates commercial invoice.
3. Invoice has number, date, due date, line items, amount, tax handling metadata and supporting milestone.
4. Record payment and allocate one payment across one/multiple invoices as allowed.
5. Recalculate outstanding balance; record proof-of-payment.
6. Reminder workflow sends approved reminder; log attempts and delivery.
7. Adjustments/credit notes use permissioned workflow and audit record.

## 12. Delivery and warranty
1. Prepare handover checklist/dossier per unit.
2. Confirm customer acceptance and outstanding conditions.
3. Record delivery date, documents, photos, recipient, odometer/condition where appropriate.
4. Warranty coverage generated from approved contract terms and start trigger.
5. Customer claim creates warranty case, evidence, assessment, disposition, repair tasks and closure.

## 13. Customer portal (later phase)
Customer user can only see explicitly shared projects, approved reports/documents, selected progress/forecast, questions/change approvals, invoices/outstanding and warranty cases. Every shared item uses explicit permission and expiry/revocation.

## 14. Global interaction states
Every key workflow needs: loading, empty, success, validation error, permission denied, conflict/stale version, processing, retryable failure, terminal failure, offline/queued action (where supported). Do not show false successful state before backend confirmation.
