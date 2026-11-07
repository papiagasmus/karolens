# 06 — Implementation Plan Document

## Document control
- Product: Karolens
- Version: 1.0-draft
- Date: 2026-11-07
- Coding gate: **not approved until all six documents are reviewed and baseline decisions are closed**.

## Phase 0 — Specification approval and readiness
- Review six documents together; map requirements across flows, UI, schema and tests.
- Choose first karoseri subsegment and one reference project scenario.
- Inspect repository and select frontend framework/toolchain.
- Confirm Supabase project/environment, backups, Auth, Storage and secrets handling.
- Confirm Cloudflare account, products, domain, pricing/limits and deployment path.
- Finalize roles/approval matrix and RLS policy matrix.
- Validate legal requirement registry with source/effective dates and assign an owner.
- Accountant validates price/tax assumptions and display treatment.
**Exit:** approved v1.0 documents, architecture decisions, no blockers affecting MVP foundations.

## Phase 1 — Foundation
- Repository baseline, lint/typecheck/test/build and CI.
- App shell, auth, organization setup, invitations and membership/role model.
- Supabase migrations for tenant foundation; RLS/storage policies tested.
- Audit events, error handling, structured logging, environment config.
**Exit:** tenant isolation and authenticated workspace verified automatically.

## Phase 2 — Project and document workspace
- Customer/project/unit CRUD.
- Private document storage and immutable versions.
- Upload validation, metadata, annotations and document links.
- Background processing job model; begin with provider-agnostic/manual extraction.
- Candidate fact extraction and human verification/approval with source traceability.
**Exit:** users upload supported files, review extracted facts and approve baseline while preserving source/version lineage.

## Phase 3 — Contract and engineering baseline
- Contract versions and clause register.
- Obligation/milestone capture and approval.
- Specification revision, baseline and change request.
- BOM revision tied to approved specification.
- Impact comparison for changes.
**Exit:** changes leave traceable audit records; AI cannot approve.

## Phase 4 — Materials, procurement and production
- Material catalog, stock visibility, reservation and shortage calculation.
- Purchase request and receipt workflow.
- Operations, dependencies, capacity calendar, progress logs, blockers and delivery forecast.
**Exit:** project owner can explain forecast from recorded blockers/events.

## Phase 5 — Compliance, quality and release
- Versioned requirement sources and applicability profiles.
- Project/unit compliance register, evidence and external-process tracking.
- Inspection templates/results, nonconformity/rework and release approval.
**Exit:** release readiness derives from applicable evidence and authorized approvals; no false claim of government approval.

## Phase 6 — Customer reporting and finance
- Customer report assembly, redaction and approval.
- Commercial invoices and milestone billing.
- Payments, allocations, receivable balances and reminders.
- Delivery dossier, acceptance and warranty workflow.
**Exit:** outputs are auditable and internal confidential data remains restricted.

## Phase 7 — Pilot and hardening
- E2E tests with synthetic or authorized pilot data.
- Mobile/tablet usability, performance, accessibility, backup/restore and security review.
- Tenant-boundary and prompt-injection testing, file-safety checks.
- Usage budgets for storage, AI, email and compute; rate limits/alerts.
- User docs, support runbook, incident and rollback plan.
**Exit:** release gate passes; owner approves controlled pilot.

## Phase 8 — Post-MVP expansion
- Customer portal with granular sharing.
- WhatsApp/email integrations.
- OEM templates/partner and government portal integration only when official support is validated.
- Advanced MRP/capacity optimization, CAD workflows, analytics and e-tax integration.

## Test/release gates
- Each migration applies cleanly to empty test DB and is reviewed.
- RLS proves cross-tenant reads/writes denied.
- Storage tests cover upload/download/version/expiry/revocation.
- Workflow tests cover draft/review/approve/supersede/reject.
- Critical calculations (BOM, costs, balances, schedule) have deterministic tests.
- AI extraction schema/source citation/untrusted document injection/human approval tests.
- E2E project lifecycle tests on mobile and desktop.
- No release with critical security, data integrity, backup or compliance blockers.

## Work management
Create small issues linked to PRD requirement IDs. Use short-lived feature branches and PRs. Migrations additive and ordered. No broad direct pushes to production branch for application features. Each PR includes tests, migration impact, security considerations and UI screenshots where applicable.

## Dependencies and risks
- First body type determines specification/BOM/regulatory templates.
- Parsing quality and AI cost may constrain the feature set.
- Regulatory source maintenance needs a named owner.
- Cloudflare product/domain configuration follows repository stack inspection.
- Tax treatment for individual business vs future PT and PKP status must be rechecked before billing launch.
- Rp1m net target at Rp1.12m final price must be modeled against actual taxes/payment fees; do not guarantee until verified.
