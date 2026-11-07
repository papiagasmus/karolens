# 02 — Technical Requirements Document (TRD)

## Document control
- Product: Karolens | Version: 1.0-draft | Date: 2026-11-07
- Status: Draft; validate against actual repository/tool versions before implementation.

## 1. Architecture principles
- Keep the first release simple: web/PWA application, Supabase managed backend, Cloudflare edge/static hosting.
- Supabase Postgres is the transactional source of truth; Supabase Auth identifies users; Storage stores uploaded source files; Edge Functions/background processing handle trusted server-side jobs.
- Cloudflare serves the app and edge/API needs where justified; do not duplicate transactional data in D1 when Postgres is already authoritative.
- All AI operations are asynchronous, metered, auditable, and provider-agnostic behind an adapter.
- Avoid vendor lock-in in file metadata, AI job definitions, and document extraction results.

## 2. Proposed stack (to validate in repository)
- Frontend: TypeScript + React; choose Vite SPA/PWA or Next.js only after checking current repo and deployment constraints. Prefer a lean PWA if no SSR/business reason requires Next.js.
- UI: Tailwind CSS and accessible component primitives; responsive/mobile-first.
- Data fetching/state: typed API client and query cache; forms with runtime schema validation.
- Backend: Supabase Postgres, Auth, Storage, Edge Functions.
- Hosting: Cloudflare Workers with Static Assets for a new static/PWA application. If Next.js is selected, follow current Cloudflare-supported Next.js deployment approach; do not assume legacy adapter compatibility.
- CI: GitHub Actions or a currently available CI provider; lint, typecheck, unit tests, migration checks, build, security checks.

## 3. Environments
- Local: local frontend and Supabase CLI stack or isolated dev project.
- Development: Supabase project `karolens` currently exists; confirm intended use and secrets before migrations.
- Preview: branch/preview deployment with isolated configuration; avoid production customer data.
- Production: separate credentials and environment, deployment approval, backups, alerting.

## 4. Identity and authorization
Roles are tenant-scoped and may include owner/admin, management, sales, project manager, engineering, PPIC, procurement, warehouse, production, QC, compliance, finance, and customer viewer. Authorization decisions must derive from trusted membership records/app metadata, never user-editable user_metadata. Enforce both role and tenant membership in server/database policies. Customer portal identities must have explicitly restricted project/document permissions.

## 5. Tenant isolation and RLS
Every tenant-owned record carries `organization_id` and relevant parent references. RLS is enabled on all exposed tables. Policies must verify membership in the same organization and role/action permissions. Do not rely on `TO authenticated` alone. Use a dedicated membership table and helper functions only if their security model is reviewed; avoid SECURITY DEFINER unless strictly necessary, with explicit grants and safe search_path. Views exposed to clients use `security_invoker = true` where supported.

## 6. File/document processing
- Private storage buckets; paths are tenant/project scoped and not directly guessable.
- Validate MIME type using file signature where practical, extension, size, malware scanning strategy, and upload permissions.
- Store checksum, original file name, storage key, MIME, byte count, version, classification, retention and uploader.
- Generate short-lived signed URLs only after authorization.
- Processing pipeline: upload -> queued job -> parse/OCR/vision extraction -> normalized candidate facts -> source citations -> human review -> approval/baseline.
- Retry transient errors with bounded retries and idempotency keys; record provider/model/version, usage/cost, status, and failure category.
- Native CAD parsing excluded until a supported parser and acceptance tests are selected.

## 7. AI service boundary
Create provider interface for document text extraction, image understanding, structured extraction and question answering. Require structured schemas and source references. Prompts include untrusted-data boundary: contents from uploads are data, not instructions. Prevent prompt injection from uploaded files from causing tool execution or data disclosure. Retrieval must scope every query to authorized tenant and project before retrieval. Do not mix tenant indexes. Avoid training/provider retention where contract and privacy needs require; review each provider's data terms.

AI-generated output labels: draft/candidate, never approved. Human actions recorded with actor/time and reason. Confidence alone is not approval. Critical facts (dimensions, vehicle weights, material specs, prices, deadlines, legal obligation) require explicit confirmation.

## 8. Data integrity and workflow
- Use Postgres transactions for multi-row state transitions.
- Prefer explicit workflow state enums and transition functions guarded by role and preconditions.
- Maintain append-only audit events for approvals, changes, status, payment allocation, release and document lineage.
- Use optimistic concurrency/version checks for specifications, contracts, documents and BOM.
- Avoid destructive overwrite of approved contract/specification baseline; create new revisions and change records.
- Use idempotent background jobs for extraction, reminders, report generation and integrations.

## 9. Integration boundaries
- Email notifications: provider to be selected; queue sends and log delivery outcomes.
- WhatsApp: later phase; use approved provider/API and consent/opt-out handling.
- Government Kemenhub portals: tracking/evidence preparation first; integration only if authorized stable API exists and terms permit.
- OEM portals/checklists: configurable requirement sets and manual evidence capture before any partner integration.
- Tax: commercial billing first; Faktur Pajak/e-tax integration later after provider and legal review.

## 10. Security, privacy, compliance
- TLS in transit; managed encryption at rest; secrets only in secret manager/environment bindings.
- Never ship Supabase service-role or Cloudflare API token to browser.
- Use publishable Supabase key in client; all privileged operations server side.
- Auth: secure session handling, MFA option for owner/admin, rate limiting, invite controls, session revocation plan.
- Audit access to sensitive contracts, drawings, and finance records.
- Export/delete/retention policy; legal hold support may be required.
- File safety: malware scanning/quarantine and safe preview/download policy.
- Backup/restore and incident response documented before production.

## 11. Observability and operations
Structured logs with tenant-safe identifiers (avoid document content/secrets), request IDs, job IDs, error categories, latency, usage/cost. Metrics: queue depth/age, extraction success, failed jobs, storage usage, auth failures, API latency, database connections, AI spend, email delivery, billing reconciliation. Alerts on queue stalls, repeated job failure, storage/AI budget thresholds, suspicious access and backup failures.

## 12. Performance and scale
Start with indexed Postgres relations and pagination. Use full-text/pgvector only when retrieval benchmarks justify; keep vector filters tenant/project scoped. Do not pre-optimize with separate search infrastructure until query performance and retrieval quality show need. Large files processed asynchronously; chunking and extraction outputs stored separately from source files.

## 13. Testing strategy
Unit tests for calculations/state transitions; integration tests for RLS/membership/file access; contract tests for API schemas; adversarial tests for cross-tenant access and prompt injection; end-to-end tests for full lifecycle; migration tests on clean DB; backup/restore exercise; mobile browser checks. Fixtures must not contain real customer-sensitive data.

## 14. Deployment/release
Build immutable artifacts; configure per-environment variables/secrets; deploy preview then staging then production. Database schema changes are migration-managed and backward-compatible (expand/contract). Deploy frontend and functions with explicit versioning. Rollback code independently from data migrations; document forward-fix strategy for irreversible migrations.

## 15. Technical decisions still open
- Frontend framework choice after inspect repo.
- File storage: Supabase Storage vs Cloudflare R2; select based on signed access, egress, cost and operational simplicity; avoid two canonical file stores.
- Document parsing/OCR and AI provider.
- Background job mechanism (Supabase queue/pgmq vs managed queue) based on retries, workload, and cost.
- Cloudflare deployment mode and domain.
- Retention, data residency, and customer contract requirements.
