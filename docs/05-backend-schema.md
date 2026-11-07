# 05 — Backend Schema Document

## Document control
- Product: Karolens | Version: 1.0-draft | Date: 2026-11-07
- This is a logical schema proposal, not a migration. Inspect and approve before DDL.

## 1. Data conventions
- PostgreSQL; UUID primary keys; `timestamptz` for event times; `numeric` for money/quantities where precision matters; ISO currency code (IDR initially).
- Tenant-owned records include `organization_id`; project/unit references enforce tenant consistency.
- Use created/updated actor IDs where relevant; immutable audit/event records for important transitions.
- Store source file bytes in private object storage; database stores metadata, extraction, lineage and permissions.
- Soft deletion only where business/legal retention permits; never silently delete contract/approval/audit history.

## 2. Identity and tenancy
- `organizations`: legal/business identity, business profile, timezone, status.
- `organization_members`: `organization_id`, `user_id`, role, membership status, invited_by, timestamps; unique organization/user.
- `role_permissions` (optional if static role matrix is sufficient): role/action grants.
- `customer_contacts`: contacts linked to customer, not auth membership unless explicitly invited as customer portal user.

## 3. CRM and projects
- `customers`: organization, legal/trading name, identifiers, address/contact metadata.
- `customer_contacts`: customer, name, email/phone, role.
- `projects`: organization, customer, project code, title, type/body category, owner, status, target/forecast dates, currency, commercial summary with field-level access control.
- `project_units`: project, unit sequence, chassis/VIN/engine identifiers when applicable, vehicle category, OEM/model, unit status.
- `project_milestones`: project/unit, milestone type, planned/actual date, status, evidence reference.
- `project_events`: normalized activity events.

## 4. Documents and knowledge
- `project_documents`: tenant/project, category, title, current version pointer, visibility, retention class.
- `document_versions`: document, version number, storage bucket/key, original filename, MIME, size, checksum, uploader, uploaded_at, source metadata, supersedes_version_id.
- `document_processing_jobs`: version, status, provider/model, idempotency key, attempts, cost/usage, error category, started/completed times.
- `document_extractions`: version/job, extraction type, structured JSON, text, confidence/quality metrics, parser version.
- `document_facts`: project/document version, fact type/key/value, source page/region/cell, confidence, status, reviewer, verified/approved times.
- `document_annotations`: page/region, comment, author, visibility.
- `document_links`: relation from document/version to project/unit/contract/spec/BOM/requirement/invoice.
- `knowledge_chunks`: chunked text, source version, page/region, embedding/provider metadata; tenant/project filter required. Could be deferred until retrieval need is validated.

## 5. Contract and change control
- `contracts`: project, customer reference, status, current approved version.
- `contract_versions`: version, storage source, status, effective/signed dates, checksum.
- `contract_clauses`: version, clause type, text, extracted structured value, source location, review status.
- `contract_obligations`: linked clause, owner, obligation type, due date/trigger, status, evidence and risk.
- `contract_milestones`: payment/delivery/acceptance milestone, amount/percentage, conditions, planned/actual dates.
- `change_orders`: project, requestor, reason, scope/cost/schedule impact, status, approval history.
- `customer_approvals`: requested decision, object/version, approver, decision, timestamp, evidence.

## 6. Engineering and material planning
- `specification_revisions`: project/unit configuration, version, status, source docs, approved_by/at.
- `specification_items`: revision, key, value, unit, tolerance, source fact, criticality.
- `bom_revisions`: project/unit/spec revision, version, status, approved_by/at.
- `bom_items`: BOM revision, item/master material, quantity, unit, waste factor, operation/fitment note.
- `materials`: organization-scoped catalog, code, description, unit, category, preferred supplier, active flag.
- `inventory_locations`: warehouse/site.
- `inventory_lots`: material, location, lot, quantity_on_hand, quality status, received date.
- `inventory_reservations`: project/unit/BOM item, lot, quantity, status.
- `purchase_requests`: project, requester, required_by, status, reason.
- `purchase_request_items`: material, quantity, spec/BOM link.
- `purchase_orders` and `purchase_order_items`: supplier order records (may be manual/imported in MVP).
- `goods_receipts` and `goods_receipt_items`: received quantities, inspection and lot linkage.

## 7. Schedule and production
- `production_operations`: project/unit, operation code/name, sequence, dependencies, work center/resource, planned/actual dates, status, progress, standard/actual hours.
- `production_logs`: operation, actor, event time, quantity/progress, notes, photos/doc links.
- `production_blockers`: project/operation, category, severity, owner, opened/resolved timestamps, impact estimate.
- `capacity_calendars`: work center/resource, date, available capacity.

## 8. Regulatory and quality
- `requirement_sources`: issuing authority/organization, source type (regulation/OEM/contract/SOP), citation, version, published/effective/expiry dates, reviewed_at.
- `requirement_templates`: source, title, applicability logic/version, vehicle/company scope, mandatory flag.
- `project_requirements`: project/unit, template/source, applicability status and rationale, owner, due date, workflow status.
- `requirement_evidence`: requirement, document/version, evidence type, verifier, verified_at, external reference/status.
- `compliance_submissions`: external portal/process name, application/reference number, submitted date, status, fee metadata, due date, outcome/evidence.
- `inspection_templates`: template type (OEM/customer/internal/regulatory), vehicle/body applicability, version.
- `inspection_items`: template item, criterion, limits/units, criticality.
- `inspections`: project/unit, template version, inspector, started/completed, overall result.
- `inspection_results`: inspection/item, result, measured value, notes, evidence.
- `nonconformities`: inspection/project/operation, severity, disposition, corrective action, closure.
- `release_approvals`: unit, gate result, approver, timestamp, exception reason, dossier version.

## 9. Reporting, billing, delivery and after-sales
- `customer_reports`: project, type, period, generated snapshot, status, approver, approved_at.
- `report_deliveries`: report, channel, recipient, sent_at, delivery state, reference.
- `customer_messages`: project, sender, channel, direction, body/reference, linked tasks.
- `invoices`: project/customer, invoice number, issue/due date, currency, subtotal, discount, tax metadata, total, status, commercial vs tax-document classification.
- `invoice_items`: invoice, description, quantity, unit price, amount, milestone reference.
- `payments`: customer, received date, amount, method, reference, proof document.
- `payment_allocations`: payment, invoice, allocated amount.
- `receivable_events`: invoice, event type, amount/status changes, actor, timestamp.
- `delivery_dossiers`: unit, checklist version, document bundle, approved_by/at.
- `delivery_records`: unit, delivered_at, recipient, acceptance state, evidence.
- `warranty_terms`: project/unit, duration, start trigger/date, coverage/exclusions from approved contract.
- `warranty_cases`: unit, opened_at, issue, claim status, assessment, resolution, closed_at.

## 10. Security, audit and platform
- `audit_events`: organization, actor, action, object type/id, before/after summary, reason, request ID, timestamp; append-only.
- `notifications`: tenant, recipient, type, payload, read/sent states.
- `background_jobs`: job type, tenant/project scope, idempotency key, state, attempt, schedule, error.
- `customer_portal_users` and `document_shares`: later phase, explicit scoped permissions, expiry and revocation.

## 11. Core relationships
Organization 1:N customers/projects/members/materials. Customer 1:N projects. Project 1:N units/documents/contracts/milestones/operations/requirements/invoices/reports. Document 1:N versions; version 1:N extraction/facts. Contract 1:N versions; version 1:N clauses; clause 1:N obligations. Specification revision 1:N spec items and BOM revisions. BOM revision 1:N BOM items. Unit 1:N inspections/release/delivery/warranty.

## 12. RLS and index requirements
Enable RLS on every exposed tenant table. Policy predicates must validate current authenticated user membership in matching `organization_id` and action permission. Verify parent/foreign-row tenant consistency on writes. Private storage policies mirror tenant/project permissions. Add indexes for tenant_id + common filter/sort columns, project_id, customer_id, unit_id, status, due dates, version IDs, storage key/checksum, and foreign keys. Use composite uniqueness for project code per organization, document version number per document, invoice number per organization, and material code per organization.

## 13. Migration sequencing (logical)
1. Tenant, membership, customer, project, units.
2. Documents, versions, jobs, extraction/facts, audit.
3. Contract versions, clauses, obligations, change approvals.
4. Specifications, BOM, materials, stock, procurement.
5. Schedule, production, blockers.
6. Requirement source library, compliance evidence, QC/release.
7. Reports, billing, payments, delivery, warranty.
8. Portal sharing and integrations later.

No SQL migration should be generated from this document until entity fields, constraints, RLS policy matrix, and indexes are reviewed.
