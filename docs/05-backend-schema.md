# 05 — Backend Schema Document

## Document control
- Product: Karolens
- Version: 1.0-draft
- Date: 2026-11-07
- Logical schema proposal only; not a migration.

## Product scope alignment
The data model must support all karoseri types from launch. Product types are extensible reference/configuration data (including tenant-defined custom types), never a closed enum. Every type can use a prebuilt or generic/custom profile and participate in the common project lifecycle.

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

## 4. Product types and reusable configuration templates
- `product_type_definitions`: extensible catalogue of karoseri types/families. `organization_id` is null only for platform-provided, read-only catalogue entries; tenant-defined/custom entries carry the owning organization. Store code, display name, family, description, active/system flags and audit metadata. Do not use a closed enum for body types.
- `product_templates`: reusable template identity scoped to a product type and template purpose, such as specification, BOM, production route, inspection/QC, compliance applicability or release dossier. May be platform-provided or tenant-owned.
- `product_template_versions`: immutable version records for each template. Store the validated configuration/schema as JSONB (typed fields, labels, units, constraints, options, conditional visibility, sequence, and references to controlled workflow items), version, status, effective dates, author/approver and change reason. Never execute arbitrary code from JSONB.
- `project_product_profiles`: organization, project, optional project unit, product type definition, selected profile/configuration, approved configuration snapshot, revision/status and approval metadata. Support project-level defaults and unit-level overrides; unit-level assignments allow mixed product types in one project.
- `project_template_assignments`: product profile, purpose/template role, exact `product_template_versions` reference, and immutable assigned snapshot. Enables a project to use different versioned templates for specification, BOM, route, QC, compliance and release.

The existing `projects.body_category` may remain as a human-readable compatibility/display field during migration, but it must not become an exhaustive enum or the authoritative product-type model. Product identity and versioned configuration are represented by the definitions/profiles above. Existing specification, BOM, operation, inspection and requirement records should retain the source profile/template version where relevant.

## 5. Documents and knowledge
- `project_documents`: tenant/project, category, title, current-version pointer, visibility and retention class.
- `document_versions`: document, version number, bucket/key, filename, MIME, size, checksum, uploader/time, source metadata and superseded version.
- `document_processing_jobs`: version, status, provider/model, idempotency key, attempts, usage/cost, error category, start/finish.
- `document_extractions`: version/job, extraction type, structured JSON/text, quality/confidence metrics and parser version.
- `document_facts`: project/document version, fact type/key/value, source page/region/cell, confidence, status, reviewer and approval timestamps.
- `document_annotations`: page/region, comment, author, visibility.
- `document_links`: link document/version to project/unit/contract/spec/BOM/requirement/invoice.
- `knowledge_chunks`: chunked text, source version/page/region and embedding/provider metadata; defer until retrieval benchmarks justify.

## 6. Contract/change control
- `contracts`: project, customer reference, status, current approved version.
- `contract_versions`: version, storage source, status, effective/signed dates and checksum.
- `contract_clauses`: version, type, text, extracted value, source location, review status.
- `contract_obligations`: clause, owner, type, due date/trigger, status and evidence/risk.
- `contract_milestones`: payment/delivery/acceptance milestone, amount/percentage, conditions and dates.
- `change_orders`: project, requester, reason, scope/cost/schedule impact, status.
- `customer_approvals`: object/version, requested decision, approver, decision, timestamp, evidence.

## 7. Engineering/material planning
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

## 8. Schedule and production
- `production_operations`: project/unit, operation, sequence, dependency, work center/resource, planned/actual dates, status/progress/hours.
- `production_logs`: operation, actor, time, quantity/progress, notes and photos/doc links.
- `production_blockers`: project/operation, category, severity, owner, open/resolve times and impact estimate.
- `capacity_calendars`: work center/resource, date and available capacity.

## 9. Regulatory and quality
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

## 10. Reports, billing, delivery and after-sales
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

## 11. Security/audit/platform
- `audit_events`: organization, actor, action, object type/id, before/after summary, reason, request ID and timestamp; append-only.
- `notifications`: tenant, recipient, type, payload and read/sent state.
- `background_jobs`: type, tenant/project scope, idempotency key, state, attempts, schedule and error.
- `customer_portal_users` / `document_shares`: later phase; explicit scoped permissions, expiry/revocation.

## 12. Relationships
Organization 1:N customers/projects/members/materials. Customer 1:N projects. Project 1:N units/documents/contracts/milestones/operations/requirements/invoices/reports. Document 1:N versions; version 1:N extractions/facts. Contract 1:N versions; version 1:N clauses; clause 1:N obligations. Specification revision 1:N items/BOM revisions; BOM revision 1:N items. Unit 1:N inspections/release/delivery/warranty.

## 13. RLS and indexes
Enable RLS on every exposed tenant table. Policies validate authenticated user membership in matching organization and role/action permission. Validate parent/child tenant consistency on writes. Private storage policies mirror tenant/project permissions. Platform catalogue/template rows (`organization_id IS NULL`) are read-only to tenant users; tenant-defined types/templates are visible only to their owning organization. Policies must not let a tenant alter global rows or read another tenant's custom definitions. Index organization + common filter/sort columns, project/customer/unit IDs, status, due dates, version IDs, checksum and foreign keys. Composite uniqueness: project code per organization, version number per document, invoice number per organization, material code per organization.

## 14. Migration sequence (logical)
1. Tenant, membership and base organization security.
2. Product-type definitions and reusable template identities/versions, with system-versus-tenant ownership and RLS tests.
3. Customer, project and unit foundation.
4. Project product profiles and immutable template assignments/snapshots.
5. Documents, versions, jobs, extraction/facts and audit.
6. Contracts, clauses, obligations, changes and approvals.
7. Specifications, BOM, materials, stock and procurement, linked to product profiles/template versions.
8. Schedule, production and blockers, including configurable production-route templates.
9. Requirement source library, compliance evidence, QC and release, linked to applicable templates.
10. Reports, billing, payments, delivery and warranty.
11. Portal sharing/integrations later.

Do not generate SQL until entity fields, constraints, RLS matrix, and indexes are reviewed.
