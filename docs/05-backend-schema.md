# 05 — Backend Schema Document

## Document control
- Product: Karolens
- Version: 1.0-draft
- Date: 2026-11-07
- Logical schema proposal only; not a migration.

## 1. Conventions
PostgreSQL; UUID primary keys; `timestamptz`; `numeric` for monetary/quantity precision; ISO currency (IDR initially). Tenant-owned rows include `organization_id`. Store original bytes in private object storage; DB contains metadata/lineage/permissions. Preserve contract, approval and audit history.

## 2. Identity and tenancy
- `organizations`: legal/business identity, business profile, timezone, status.
- `organization_members`: organization, user, role, membership status, inviter, timestamps; unique organization/user.
- `role_permissions` (optional when static role matrix is insufficient).

## 3. CRM and projects
- `customers`: organization, legal/trading name, identifiers and address/contact metadata.
- `customer_contacts`: customer, name, email/phone, role.
- `projects`: organization, customer, code, title, body category, owner, status, target/forecast dates, currency and restricted commercial summary.
- `project_units`: project, unit sequence, chassis/VIN/engine identifiers where relevant, vehicle category/OEM/model/status.
- `project_milestones`: project/unit, type, planned/actual date, status, evidence.
- `project_events`: normalized activity events.

## 4. Documents and knowledge
- `project_documents`: tenant/project, category, title, current-version pointer, visibility and retention class.
- `document_versions`: document, version number, bucket/key, filename, MIME, size, checksum, uploader/time, source metadata and superseded version.
- `document_processing_jobs`: version, status, provider/model, idempotency key, attempts, usage/cost, error category, start/finish.
- `document_extractions`: version/job, extraction type, structured JSON/text, quality/confidence metrics and parser version.
- `document_facts`: project/document version, fact type/key/value, source page/region/cell, confidence, status, reviewer and approval timestamps.
- `document_annotations`: page/region, comment, author, visibility.
- `document_links`: link document/version to project/unit/contract/spec/BOM/requirement/invoice.
- `knowledge_chunks`: chunked text, source version/page/region and embedding/provider metadata; defer until retrieval benchmarks justify.

## 5. Contract/change control
- `contracts`: project, customer reference, status, current approved version.
- `contract_versions`: version, storage source, status, effective/signed dates and checksum.
- `contract_clauses`: version, type, text, extracted value, source location, review status.
- `contract_obligations`: clause, owner, type, due date/trigger, status and evidence/risk.
- `contract_milestones`: payment/delivery/acceptance milestone, amount/percentage, conditions and dates.
- `change_orders`: project, requester, reason, scope/cost/schedule impact, status.
- `customer_approvals`: object/version, requested decision, approver, decision, timestamp, evidence.

## 6. Engineering/material planning
- `specification_revisions`: project/unit configuration, version, status, source docs, approved_by/at.
- `specification_items`: revision, key, value, unit, tolerance, source fact, criticality.
- `bom_revisions`: project/unit/spec revision, version, status, approver.
- `bom_items`: BOM revision, material, quantity, unit, waste factor and operation note.
- `materials`: organization catalog, code, description, unit, category, supplier preference, active.
- `inventory_locations`: warehouse/site.
- `inventory_lots`: material, location, lot, on-hand quantity, quality status, received date.
- `inventory_reservations`: project/unit/BOM item, lot, quantity, status.
- `purchase_requests` / `purchase_request_items`: project, requester, required-by, status, material and quantity.
- `purchase_orders` / `purchase_order_items`: supplier orders, manual/imported initially.
- `goods_receipts` / `goods_receipt_items`: received quantity, inspection and lot link.

## 7. Schedule and production
- `production_operations`: project/unit, operation, sequence, dependency, work center/resource, planned/actual dates, status/progress/hours.
- `production_logs`: operation, actor, time, quantity/progress, notes and photos/doc links.
- `production_blockers`: project/operation, category, severity, owner, open/resolve times and impact estimate.
- `capacity_calendars`: work center/resource, date and available capacity.

## 8. Regulatory and quality
- `requirement_sources`: issuer, source type (regulation/OEM/contract/SOP), citation, version, publication/effective/expiry dates and review date.
- `requirement_templates`: source, title, versioned applicability logic, vehicle/company scope and mandatory flag.
- `project_requirements`: project/unit, template/source, applicability status/rationale, owner, due date and workflow status.
- `requirement_evidence`: requirement, document/version, evidence type, verifier/time and external reference/status.
- `compliance_submissions`: external process, application/reference number, submitted date, status, fee metadata, due date and outcome evidence.
- `inspection_templates` / `inspection_items`: template type/version, applicability, criteria, limits/units and criticality.
- `inspections`: project/unit, template, inspector, start/finish and result.
- `inspection_results`: inspection/item, result, measured value, notes and evidence.
- `nonconformities`: inspection/project/operation, severity, disposition, corrective action and closure.
- `release_approvals`: unit, gate result, approver/time, exception reason and dossier version.

## 9. Reports, billing, delivery and after-sales
- `customer_reports`: project, type, period, generated snapshot, status, approver/time.
- `report_deliveries`: report, channel, recipient, sent time, delivery status/reference.
- `customer_messages`: project, sender/channel/direction, body/reference and linked tasks.
- `invoices`: project/customer, number, issue/due dates, currency, subtotal/discount/tax metadata/total/status, commercial-vs-tax document classification.
- `invoice_items`: invoice, description, quantity, unit price, amount and milestone.
- `payments`: customer, received date, amount, method, reference and proof document.
- `payment_allocations`: payment, invoice and allocated amount.
- `receivable_events`: invoice, event type, amount/status, actor and time.
- `delivery_dossiers`: unit, checklist version, document bundle, approver/time.
- `delivery_records`: unit, delivery date, recipient, acceptance state and evidence.
- `warranty_terms`: project/unit, duration, start trigger/date, coverage/exclusions from approved contract.
- `warranty_cases`: unit, opened date, issue, claim status, assessment, resolution and closure.

## 10. Security/audit/platform
- `audit_events`: organization, actor, action, object type/id, before/after summary, reason, request ID and timestamp; append-only.
- `notifications`: tenant, recipient, type, payload and read/sent state.
- `background_jobs`: type, tenant/project scope, idempotency key, state, attempts, schedule and error.
- `customer_portal_users` / `document_shares`: later phase; explicit scoped permissions, expiry/revocation.

## 11. Relationships
Organization 1:N customers/projects/members/materials. Customer 1:N projects. Project 1:N units/documents/contracts/milestones/operations/requirements/invoices/reports. Document 1:N versions; version 1:N extractions/facts. Contract 1:N versions; version 1:N clauses; clause 1:N obligations. Specification revision 1:N items/BOM revisions; BOM revision 1:N items. Unit 1:N inspections/release/delivery/warranty.

## 12. RLS and indexes
Enable RLS on every exposed tenant table. Policies validate authenticated user membership in matching organization and role/action permission. Validate parent/child tenant consistency on writes. Private storage policies mirror tenant/project permissions. Index organization + common filter/sort columns, project/customer/unit IDs, status, due dates, version IDs, checksum and foreign keys. Composite uniqueness: project code per organization, version number per document, invoice number per organization, material code per organization.

## 13. Migration sequence (logical)
1. Tenant, membership, customer, project, units.
2. Documents, versions, jobs, extraction/facts, audit.
3. Contracts, clauses, obligations, changes/approvals.
4. Specifications, BOM, materials, stock, procurement.
5. Schedule, production, blockers.
6. Requirement source library, compliance evidence, QC/release.
7. Reports, billing, payments, delivery, warranty.
8. Portal sharing/integrations later.

Do not generate SQL until entity fields, constraints, RLS matrix, and indexes are reviewed.
