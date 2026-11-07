# 02 — Technical Requirements Document (TRD)

## Document control
- Product: Karolens
- Version: 1.0-draft
- Date: 2026-11-07
- Validate all versions and deployment assumptions against the repository before implementation.

## 1. Architecture principles
- Keep the first release simple: web/PWA app, Supabase managed backend, Cloudflare hosting/edge where justified.
- Supabase Postgres is transactional source of truth; Supabase Auth identifies users; Storage stores uploaded source files; Edge Functions/background jobs process trusted server-side tasks.
- Cloudflare serves the app and edge/API needs where justified; do not duplicate transactional data in D1 when Postgres is authoritative.
- AI operations are asynchronous, metered, auditable, and provider-agnostic behind an adapter.
- Avoid vendor lock-in in file metadata, AI job definitions, and extraction results.

## 2. Universal product-type configuration
The architecture MUST support all karoseri types from launch. Product type is configuration/reference data, not a closed application enum and not a code branch that selects a separate application workflow.

Requirements:
- Maintain an extensible product-type catalogue with platform-provided entries and tenant-defined/custom entries. Examples are seed data, never an exhaustive allow-list.
- Support reusable, versioned templates for specification fields/forms, BOM structures, production routes/operations, QC/inspection, compliance applicability, and release evidence.
- Template definitions include typed fields, labels, units, required/optional rules, validation constraints, option sets, conditional visibility, and ordering. Validate configuration against a controlled schema; do not execute arbitrary tenant-supplied code.
- Allow a project or individual unit to select a product type and assign the relevant template versions. Support mixed product types within one customer/project when the order contains different units.
- Snapshot the selected product profile and template versions on the project/unit. Later template edits must not silently mutate approved specifications, BOMs, production history, or compliance evidence.
- Permit a generic/custom profile when no prebuilt template exists. A missing template must never block quoting, project creation, the common lifecycle, or manual capture of type-specific data.
- Keep shared workflow states and authorization consistent across product types. Product-specific steps are configurable additions to the shared lifecycle, not separate applications.
- Record template source, version, effective period, author/approver, and change history. Provide an impact/revision workflow when a new template version is adopted by an active project.

The catalogue and templates must be tenant-safe. Platform templates are read-only to tenants; tenant templates are scoped to their organization. The absence of a preconfigured body type is handled with a custom profile, not by changing application code.

## 3. Proposed stack (validate after repo inspection)
- Frontend: TypeScript + React; choose Vite SPA/PWA or Next.js only after verifying requirements. Prefer a lean PWA if no SSR requirement exists.
- UI: Tailwind CSS and accessible component primitives; responsive/mobile-first.
- Data access: typed API client and query cache; forms with runtime schema validation.
- Backend: Supabase Postgres, Auth, Storage, Edge Functions.
- Hosting: Cloudflare Workers with Static Assets for a new static/PWA app. If Next.js is selected, follow current Cloudflare-supported Next.js deployment approach; do not assume legacy adapter compatibility.
- CI: GitHub Actions or currently available CI; lint, typecheck, unit tests, migration checks, build and security checks.

## 4. Environments
- Local: local frontend and Supabase CLI stack or isolated dev project.
- Development: Supabase project `karolens` exists; confirm intended environment and secrets before migrations.
- Preview: isolated configuration; avoid production customer data.
- Production: separate credentials/environment, deployment approval, backups and alerting.

## 5. Identity and authorization
Roles are tenant-scoped: owner/admin, management, sales, project manager, engineering, PPIC, procurement, warehouse, production, QC, compliance, finance, and customer viewer. Authorization derives from trusted membership records/app metadata, never user-editable `user_metadata`. Enforce both role and tenant membership in database/server policies. Customer portal identities receive explicit project/document scope only.

## 6. Tenant isolation and RLS
Every tenant-owned record carries `organization_id` and relevant parent references. Enable RLS on all exposed tables. Policies verify membership in the same organization and role/action permission. `TO authenticated` alone is not authorization. Use membership table predicates and reviewed helper functions. Avoid SECURITY DEFINER unless strictly necessary with explicit grants and safe search_path. Exposed views use `security_invoker = true` where supported.

## 7. File/document processing
- Private storage buckets; paths are tenant/project scoped and not guessable.
- Validate MIME type using file signature where practical, extension, size, upload permission, and malware scanning/quarantine strategy.
- Store checksum, original filename, storage key, MIME, byte count, version, classification, retention and uploader.
- Generate short-lived signed URLs only after authorization.
- Processing: upload -> queued job -> parse/OCR/vision extraction -> normalized candidate facts -> citations -> human review -> approval/baseline.
- Bounded retries, idempotency keys, provider/model/version, usage/cost, status and failure category.
- Native CAD parsing excluded until parser and acceptance tests selected.

## 8. AI service boundary
Provider interface for text extraction, image understanding, structured extraction and question answering. Require structured schemas and source references. Uploaded file contents are untrusted data, never instructions. Prevent prompt injection from triggering tools or cross-project disclosure. Authorize tenant/project before retrieval; never mix tenant indexes. Review provider retention/data terms before use.

AI output labels: draft/candidate, never approved. Human actions are recorded with actor/time/reason. Confidence is not approval. Critical facts (dimensions, weights, material specs, prices, deadlines, legal obligations) require explicit confirmation.

## 9. Data integrity and workflow
- Postgres transactions for multi-row state transitions.
- Explicit workflow states and guarded transitions.
- Append-only audit events for approvals, changes, status, payment allocation, release and document lineage.
- Optimistic concurrency/version checks for specifications, contracts, documents and BOM.
- Approved baselines and adopted template snapshots are never overwritten; create revisions and change records.
- Enforce referential integrity between project/unit product profiles, template versions, specification revisions, BOM revisions, operations and inspection records.
- Idempotent background jobs for extraction, reminders, report generation and integrations.

## 10. Integration boundaries
- Email notifications: provider selected later; queue sends and record delivery outcomes.
- WhatsApp: later phase with approved provider/API and consent/opt-out handling.
- Government Kemenhub portals: evidence preparation/tracking first; integrate only if authorized stable API exists and terms permit.
- OEM checklists: configurable requirement sets and manual evidence capture before partner integrations.
- Tax: commercial billing first; Faktur Pajak/e-tax integration later after provider and legal review.

## 11. Security and privacy
- TLS in transit; managed encryption at rest; secrets in server secret manager/environment bindings.
- Never expose Supabase service-role/secret key or Cloudflare API token to browser.
- Use publishable Supabase key in client; privileged operations server-side.
- Auth: secure session handling, MFA option for owner/admin, rate limits, invite controls, session revocation plan.
- Audit access to contracts, drawings and finance records.
- Export/delete/retention policy; legal hold may be required.
- File safety: malware scanning/quarantine and safe preview/download policy.
- Backup/restore and incident response documented before production.

## 12. Observability
Structured logs with tenant-safe identifiers (no document content/secrets), request/job IDs, error categories, latency, usage/cost. Metrics: queue depth/age, extraction success, failed jobs, storage use, AI spend, auth failures, API latency, email delivery, billing reconciliation. Alert on queue stalls, repeat failures, budget thresholds, suspicious access and backup failures.

## 13. Performance and scale
Start with indexed Postgres relations and pagination. Use full-text/pgvector only after retrieval benchmarks justify; keep vector filters tenant/project scoped. Avoid separate search infrastructure until query performance/retrieval quality show need. Process large files asynchronously; store chunks separately from originals.

## 14. Testing strategy
Unit tests for calculations/state transitions; integration tests for RLS/membership/file access; API contract tests; adversarial cross-tenant and prompt-injection tests; E2E full lifecycle; clean DB migration tests; backup/restore exercise; mobile browser checks. Use synthetic/authorized fixtures only. Product-configuration tests must cover materially different body families (for example dump body, tanker, bus/trailer or special-purpose) plus a tenant-defined custom type, including template versioning, mixed types in one project, and preservation of approved project snapshots. Adding a product type or template must not require a new code path for the common lifecycle.

## 15. Deployment/release
Immutable artifacts; per-environment secrets. Preview then staging then production. Schema changes migration-managed and backward-compatible (expand/contract). Version deployments; rollback code independently from data migrations and document forward-fix strategy.

## 16. Open technical decisions
- Frontend framework after repo inspection.
- File storage: Supabase Storage vs Cloudflare R2; choose one canonical store based on access control, cost and egress.
- Document parsing/OCR and AI provider.
- Background job mechanism (Supabase queue/pgmq vs managed queue).
- Cloudflare deployment mode and domain.
- Retention, residency and customer contract requirements.
