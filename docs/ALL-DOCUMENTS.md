# Karolens — Documentation Bundle

# 01 — Product Requirement Document (PRD)

## Document control
- Product: Karolens
- Version: 1.0-draft
- Date: 2026-11-07
- Status: Draft for review; not implementation approval

## 1. Product vision
Karolens is a project operating system for Indonesian vehicle-body manufacturers (karoseri), designed to support **all karoseri types from launch**. It connects customer requirements, technical knowledge, contract obligations, material planning, production, regulatory evidence, customer communications, billing, delivery, and warranty in one traceable project record. One universal platform serves conventional, specialized, and customer-defined body types; differences are handled through versioned product configurations and templates, not separate applications.

**Positioning:** The Karoseri Project & Compliance Operating System.  
**Value promise:** From customer specification to a compliant, profitable vehicle delivery.

## 2. Commercial baseline
- Customer-facing target price: **Rp1.120.000 per company per month**, one final price; do not display an additional tax surcharge on top of this target price.
- Internal net-receipt target: Rp1.000.000 per company per month after applicable taxes and fees. This is a planning goal, not a tax conclusion or guaranteed result. Model the actual individual-business and later PT tax status, PKP/VAT obligations, payment fees, and withholding treatment with an accountant before invoicing. Never encode one flat tax assumption as universal law.
- Pricing unit: customer company/workspace, not per user, unless changed in a future pricing decision.

## 3. Target users and jobs
Primary customer: Indonesian karoseri companies of different sizes and product specializations, initially prioritizing operators where coordination is fragmented across spreadsheets, paper, chat, and separate systems. The customer segment approached first is a go-to-market choice only; it does not restrict product eligibility or supported body types.

Roles: owner/director, sales/admin, project manager, engineering, PPIC/planner, purchasing, warehouse, production supervisor, QC/inspection, compliance/document control, finance/AR, and customer viewer.

Jobs to be done:
1. Understand exactly what was sold and promised.
2. Convert approved specifications into a traceable technical baseline and material/component requirements.
3. Estimate cost, monitor actual cost, and protect project margin.
4. Know the project schedule, blockers, capacity impact, and credible delivery forecast.
5. Prove regulatory, OEM, contractual, and internal quality obligations before release.
6. Keep customers informed and collect milestone payments.

## 4. Product principles
- One project, one source of truth.
- All karoseri types are within launch product scope; there is no body-type exclusion list.
- A shared lifecycle handles common work; versioned configurations/templates handle product-specific specifications, BOMs, production routes, inspections, and applicable requirements.
- A new or uncommon body type must remain manageable through a custom product profile even when no prebuilt template exists.
- Pilot and GTM prioritization must never be used as a product-scope restriction.
- Evidence before status: status changes require attributable records.
- Human approval for technical baselines, contractual interpretation, legal/compliance sign-off, and customer-facing reports.
- Distinguish law/regulation, OEM requirements, customer contract clauses, and internal SOP.
- Do not claim to issue government approvals or replace Kemenhub portals.
- Mobile-first shop-floor experience; full desktop capability for planning, finance, and document control.
- Tenant isolation by company; auditability by default.

### Universal product coverage
Karolens supports, from launch, all types of karoseri products and customer-defined variants. Examples include dump bodies, cargo/box bodies, wingbox, tankers, mixers, trailers, buses, arm-roll and hook-lift bodies, crane trucks, ambulances, fire/rescue vehicles, and other special-purpose builds. This list is illustrative, not a closed enum or eligibility list.

Every type uses the same core project lifecycle. Product-specific differences are represented through configurable and versioned product profiles and templates for specification fields, BOM structures, production routes/operations, QC inspections, compliance applicability, and release evidence. If a ready-made template is unavailable, users can start from a generic/custom profile and complete the project without waiting for a code change. Template depth may improve over time; product-type support itself is not deferred.

### Scope versus go-to-market
The product scope is all karoseri types. The first sales segment, pilot customer, and reference project are selected solely to sequence customer acquisition and validate workflows. They do not determine which product types Karolens can support.

## 5. Core product domains
1. Commercial & Project Management.
2. Project Knowledge & Document Intelligence.
3. Contract & Obligation Management.
4. Engineering & Technical Intelligence.
5. Material & Production Control.
6. Regulatory & Company Compliance.
7. Quality & Vehicle Release.
8. Customer Reporting & Communication.
9. Billing & Receivables.
10. Delivery & After-Sales.

## 6. Project workspace and uploaded knowledge
Initial supported uploads: PDF, common images, DOCX, XLSX and other explicitly validated office formats. File size/type limits are configuration decisions. Native CAD parsing is excluded from MVP until a supported parser is selected; accept PDF/image exports initially.

Each file has immutable versions, uploader, timestamp, source, checksum, project association, visibility, and review state. AI may extract text/tables/fields, summarize, identify entities, compare versions, identify potential inconsistencies, and answer project questions with citations to source file/version/page or image region where supported.

Knowledge states:
- Uploaded — stored, not analyzed.
- Extracted — machine-extracted candidate facts.
- Verified — reviewed by an authorized person.
- Approved/Baseline — formally approved source of truth.

AI-extracted information must never silently become an approved engineering specification, contract baseline, or compliance pass. Every consequential fact retains lineage to source and reviewer.

## 7. Contract obligations
Capture with human review: scope, specifications, price, payment terms, advance/progress/final milestones, delivery deadline, acceptance criteria, penalties/liquidated damages, warranty, exclusions, variation orders, dispute provisions, and signatures/versions. Approved clauses create linked obligations and reminders. AI flags possible risks; it does not provide binding legal advice or modify signed contracts.

## 8. Project planning and execution
A project links vehicle units, approved configuration/specification, BOM revisions, required materials/components, supplier/procurement records, production operations, dependencies, capacity, start/finish dates, risks, and progress evidence.

Planning exposes assumptions and confidence. Delivery forecast shows expected date plus drivers/blockers (material, engineering approval, capacity, rework, inspection, documentation, customer dependency). Avoid false precision when source data is incomplete.

## 9. Regulatory and release management
Track applicability and evidence, not generic checklists detached from context. Requirements are classified by source type: mandatory national/local regulation, OEM certification/requirement, customer contract, and company SOP. Each requirement records source, effective date/version, applicability rule, owner, required evidence, due date, verification status, and reviewer.

Karolens may prepare/checklist/track SKRB, SUT, physical test/BAP, SRUT and supporting evidence according to applicable workflows; it does not submit or issue legal approvals unless an officially supported integration is separately validated. Keep per-vehicle identity and dossier linkage. Responsibility for registration steps is configurable by contract and legal context.

## 10. Customer reports and billing
Reports: periodic progress, schedule/forecast, blockers, approved photos, milestone completion, inspection, delivery and warranty. Customer output excludes internal margin, supplier costs, internal risk notes, and restricted data unless explicitly approved.

Billing supports commercial invoices and milestone receivables. Distinguish commercial invoice from tax invoice (Faktur Pajak). E-tax integration is not MVP. Support partial payments, allocations, overdue tracking, payment evidence, and audit history.

## 11. MVP scope
MVP supports the connected workflow for **all karoseri types from launch**. The release must not require a company or project to belong to one selected subsegment. Each type can be handled with a prebuilt template, a tenant-configured template, or a generic/custom configuration:
- company workspace, users, roles, customers, projects and units;
- extensible product-type catalogue, tenant-defined/custom types, and versioned templates for specifications, BOMs, production routes, QC and compliance;
- project/unit product profiles with a durable snapshot of the selected type and template versions;
- project document upload/version/metadata and human-verified extraction;
- contract clause capture and milestone obligation register;
- specification baseline and controlled revision/change request;
- BOM/material requirement list, shortages and procurement request;
- basic milestone/operation schedule with progress, blockers and forecast;
- compliance evidence register with applicability/status and per-unit checklist;
- QC inspections, nonconformity/rework, release checklist;
- customer report draft + human approval;
- invoice milestone, payment record, receivable dashboard;
- audit log and secure file access.

Out of initial MVP: full accounting/GL, payroll, automatic legal judgement, direct government approval issuance, full CAD engine, supplier marketplace, customer self-service portal (Phase 2), complex MRP optimizer, and unsupervised AI actions.

## 12. Non-functional requirements
Security: tenant isolation, least privilege, RLS on exposed tables, private file buckets, signed access, audit trails, secure secrets. Reliability: backups/recovery plan, idempotent background processing, observable jobs. Performance: mobile-usable common screens; pagination and async document processing. Accessibility: readable contrast, keyboard operation on desktop, clear status semantics. Data portability: exports of project data and documents with metadata.

## 13. Success metrics
Activation: first customer/project created for any supported or custom body type, first file uploaded and verified, first obligation/schedule established. Track coverage by product type and template/custom-profile usage. Workflow: projects with approved baseline, BOM completeness, material shortage visibility, milestone reporting cadence, inspection evidence completeness, overdue receivables visibility. Outcomes: on-time delivery trend, rework trend, estimate-vs-actual variance, collection delay, time spent preparing customer reports. Do not claim outcome improvements until measured with real product data.

## 14. Risks and assumptions
- Karoseri workflows vary by body type, OEM, customer, and project complexity; the product must represent these differences through configurable, versioned profiles/templates rather than hard-coded single-type assumptions.
- Some product types may initially use generic/custom templates; absence of a prebuilt template must not block onboarding, project creation, or the common project lifecycle.
- Existing karoseri ERP, Odoo/custom ERP, and OEM PDI mean generic ERP/QC is not enough differentiation.
- Rp1.120.000 price and Rp1m net economics remain hypotheses, not proven willingness to pay.
- Legal requirements change and depend on vehicle category, company scale/risk, process and location.
- AI extraction may misread technical tables/drawings; approval gate and citations are mandatory.
- Customer willingness to centralize contracts and drawings depends on trust, privacy, and usability.

## 15. PRD approval criteria
- First GTM/pilot segment and representative workflows selected for acquisition sequencing only; all karoseri types remain in launch scope.
- Universal product-type configuration and custom-type fallback approved and validated across materially different body families.
- MVP boundaries approved.
- Roles and critical approval matrix agreed.
- Legal requirement source registry owner and update cadence assigned.
- Commercial model and price/tax handling reviewed by accountant.
- Each MVP requirement mapped to flow, UI, backend tables, and implementation phase.


---

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


---

# 03 — App Flow Document

## Document control
- Product: Karolens
- Version: 1.0-draft
- Date: 2026-11-07

## Product scope alignment
Karolens supports all karoseri types from launch. These flows use the same project lifecycle; body-type variation is handled by product profiles and versioned templates, with a generic/custom path for any type that has no prebuilt template. A pilot segment is a GTM choice, not a product restriction.

## 1. Navigation model
Main navigation: Dashboard, Customers, Projects, Planning & Materials, Engineering, Compliance, Quality, Billing, Reports, Documents/Knowledge, Settings. Role-based visibility is convenience only; backend authorization is authoritative.

## 2. First-time organization setup
1. Sign up / accept invitation.
2. Create organization profile: business name, address, business profile, contacts, timezone and logo.
3. Invite members and assign tenant-scoped roles.
4. Configure project numbering, IDR currency, document categories, approval matrix and notification preferences.
5. Configure company compliance profile and applicability owner.
6. Configure or review the product-type catalogue and optional templates for specifications, BOM, production routes, QC and compliance; platform-provided and tenant-defined types are both available.
7. Dashboard empty state guides first project.

## 3. Customer-to-project flow
1. Create customer/contact.
2. Create quotation/opportunity with vehicle/body type, quantity, high-level requirements and target delivery.
3. Upload request documents/drawings/contract draft.
4. Create project after order acceptance; link quote/order reference and owner.
5. Create vehicle/unit records (VIN/chassis/engine identifiers only where relevant and authorized).
6. Assign a product type to the project or each relevant unit from the extensible catalogue; select a ready-made, tenant-configured, or generic/custom profile. A missing prebuilt template never blocks the flow.
7. Capture product-specific configuration using the selected template (or custom fields), then link the approved profile to specification/BOM/production/QC/compliance records.
8. Link contract, obligations, payment milestones and acceptance criteria.

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

## 15. Product type and template management
1. Organization admins browse the extensible product-type catalogue; entries may be platform-provided or tenant-defined. The list is not a closed set of body types.
2. Admins can create a custom type/family when the required product is not listed, without requesting a code release.
3. For each type, admins can configure and version specification fields, BOM templates, production routes/operations, QC checklists, compliance applicability, and release evidence templates.
4. Templates have draft/review/approved/retired states and retain version history. Only authorized users can approve or retire templates.
5. When a project/unit is created, the user selects the product type and chooses an applicable template version or generic/custom profile. Mixed types may exist within one project.
6. The project stores a snapshot of the chosen type, configuration, and template versions. Template updates affect new assignments by default; existing approved project baselines change only through an explicit revision/impact approval.
7. During the project lifecycle, users can add custom fields or request a controlled template revision without changing the common project lifecycle.
8. Portfolio and project views consistently identify product type while preserving the same navigation and operational states across all types.


---

# 04 — Design Brief Document

## Document control
- Product: Karolens
- Version: 1.0-draft
- Date: 2026-11-07

## Product scope alignment
The experience must support all karoseri types from launch through one shared application and lifecycle. Product-specific UI is configuration-driven; no body type may be treated as unsupported because a prebuilt template is missing.

## 1. Design intent
Create a confident, premium industrial operations interface: precise, legible, calm under pressure, and optimized for decisions on desktop and mobile. Avoid a generic admin-dashboard appearance and excessive decoration.

## 2. Experience principles
- One glance: what is happening, blocked, and needs action.
- Evidence-led: status links to underlying source, approval or event.
- Progressive disclosure: summary first, technical detail on demand.
- Consistency: same lifecycle status/severity grammar across screens.
- Field-ready: large touch targets, readable typography, quick capture and resilient upload.
- Prioritize finance/engineering accuracy over decoration.

## 3. Visual direction
- Modern industrial control room; premium but practical.
- Typography: Jakarta Sans or equivalent legible sans-serif; define clear type scale and tabular numeric styles.
- Palette: neutral graphite/stone foundations with restrained blue/teal primary accent; amber warning, red critical, green verified/complete. Never rely on color alone.
- Surfaces: clean panels, subtle borders and restrained shadows. Avoid heavy glassmorphism if it harms contrast/performance.
- Charts only when they support decisions; label units, period, provenance and drill-down. The interface must work consistently across all karoseri types, with product-specific fields and sections rendered from approved configuration rather than a single body-type-specific screen set.

## 4. Responsive behavior
- Mobile: capture/review/approval/status update; compact top bar, project switcher, touch-friendly forms and sticky contextual actions.
- Tablet: split-pane operational lists/details.
- Desktop: planning grids, comparison views, contract/document editing, finance registers and dashboards.
- Avoid horizontal scrolling for common mobile tasks; specialized BOM/schedule grids use deliberate responsive alternatives.

## 5. Dashboard hierarchy
1. Portfolio health: active/at-risk projects, overdue milestones, material blockers, release-ready units, overdue receivables.
2. Action queue: approvals, shortages, inspections, expiring documents, report approvals, invoices due.
3. Portfolio: customer, body/unit type, progress, forecast, status and responsible manager.
4. Drill down to project evidence and action.

## 6. Project screen
Header: project number/name, customer, unit count, lifecycle status, forecast delivery and owner. Indicators: engineering baseline, materials, production, compliance, QC, reporting and billing. Timeline records actor/action/reason.

## 7. Component system
Tokens for color, spacing, radius, typography, shadows, focus rings and motion. Components: AppShell, Sidebar/BottomNav, PageHeader, ProjectHeader, StatusBadge, MetricCard, ActionQueue, DataTable, FilterBar, EmptyState, UploadDropzone, FileVersionStack, EvidenceCitation, ApprovalPanel, Timeline, ScheduleBoard, BOMTable, RequirementChecklist, QCResult, InvoiceSummary, ReportPreview, ConfirmDialog, Toast and Quick Search.

## 8. Status grammar
Lifecycle: Draft, Active, On Hold, At Risk, Completed, Cancelled. Review: Uploaded, Processing, Extracted, Needs Review, Verified, Approved/Baseline, Rejected, Superseded. Requirement: Not Applicable (reason required), Missing, In Progress, Submitted/External Review, Approved/Verified, Expired, Rejected. Severity: Info, Warning, Critical.

## 9. Interaction and motion
Use subtle functional transitions for navigation, panel expansion, processing progress and state changes. Respect reduced-motion preferences. Never delay data entry or obscure state with animation.

## 10. Accessibility and content
Target WCAG AA contrast. Visible keyboard focus, explicit labels/errors. Indonesian default UI; structure for localization. Explain abbreviations contextually. Dynamic fields must preserve accessible labels, units, required/error states, and keyboard order.

## 11. Screen inventory
Auth/organization setup; dashboard; customers; project list/detail; project files/knowledge; document compare/review; contract/obligation register; spec editor/version compare; BOM/material availability; schedule/production; procurement; compliance library/register; unit dossier; QC/nonconformity; report composer; invoice/receivables; delivery/warranty; users/roles/settings; product-type catalogue and template management; project/unit product configuration and template selection.

## 12. Universal product-type interaction patterns
- Use one shared project lifecycle and navigation for every body type; never fork the application into a type-specific product.
- Render product-specific forms from versioned field definitions, including labels, units, validation, required fields, and conditional sections. Preserve a predictable layout and clear provenance.
- Make product type visible in project/unit headers, portfolio rows, filters, and reports; mixed-type projects must remain understandable.
- Offer a clear generic/custom path when a type or ready-made template is missing. Do not show a dead end, disabled workflow, or message implying that the type is unsupported.
- Template selection displays its name/version and the effect of adopting it. Existing approved project snapshots remain stable unless the user performs an authorized revision.
- Design reusable views for specification, BOM, routing, inspection and compliance templates; avoid hard-coded assumptions about dimensions, components, operations, or number of checklist items.

## 13. UX acceptance checks
A supervisor records progress/photo on mobile; engineer compares drawing revisions and approves facts with source; manager explains blockers/forecast; finance sees due/received amounts; report approver detects confidential data; customer viewer cannot access internal records.


---

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


---

# 06 — Implementation Plan Document

## Document control
- Product: Karolens
- Version: 1.0-draft
- Date: 2026-11-07
- Coding gate: **not approved until all six documents are reviewed and baseline decisions are closed**.

## Product scope invariant
Karolens supports all karoseri types from launch. Implementation may sequence template depth and pilot acquisition, but may not defer support for a product type. A generic/custom profile must let any type use the shared project lifecycle even when a dedicated template is not yet available.

## Phase 0 — Specification approval and readiness
- Review six documents together; map requirements across flows, UI, schema and tests.
- Select a first GTM/pilot segment and reference customer scenario for acquisition sequencing only; this choice must not narrow product scope.
- Approve universal launch support for all karoseri types, including an extensible catalogue and generic/custom fallback when no prebuilt template exists.
- Validate the product model using multiple materially different body families and at least one tenant-defined custom type; include a mixed-type project scenario.
- Inspect repository and select frontend framework/toolchain.
- Confirm Supabase project/environment, backups, Auth, Storage and secrets handling.
- Confirm Cloudflare account, products, domain, pricing/limits and deployment path.
- Finalize roles/approval matrix and RLS policy matrix.
- Validate legal requirement registry with source/effective dates and assign an owner.
- Accountant validates price/tax assumptions and display treatment.
**Exit:** approved v1.0 documents, architecture decisions, no blockers affecting MVP foundations.

## Phase 1 — Foundation
- Repository baseline, lint/typecheck/test/build and CI.
- Extensible product-type catalogue with platform-provided and tenant-defined/custom entries; avoid closed body-type enums.
- Versioned template foundation for specification, BOM, production route, QC/inspection, compliance and release evidence; ownership, approval and RLS rules.
- Generic/custom product profile that permits any karoseri type to enter the common lifecycle without a prebuilt template.
- App shell, auth, organization setup, invitations and membership/role model.
- Supabase migrations for tenant foundation; RLS/storage policies tested.
- Audit events, error handling, structured logging, environment config.
**Exit:** tenant isolation and authenticated workspace verified automatically.

## Phase 2 — Project and document workspace
- Customer/project/unit CRUD across all product types.
- Assign product profiles at project or unit level, including mixed-type units within one project; snapshot selected template versions.
- Private document storage and immutable versions.
- Upload validation, metadata, annotations and document links.
- Background processing job model; begin with provider-agnostic/manual extraction.
- Candidate fact extraction and human verification/approval with source traceability.
**Exit:** users upload supported files, review extracted facts and approve baseline while preserving source/version lineage.

## Phase 3 — Contract and engineering baseline
- Contract versions and clause register.
- Dynamic, validated specification capture from the selected product profile/template, with manual/custom fallback.
- BOM template selection and revision linkage to the approved product/specification baseline.
- Obligation/milestone capture and approval.
- Specification revision, baseline and change request.
- BOM revision tied to approved specification.
- Impact comparison for changes.
**Exit:** changes leave traceable audit records; AI cannot approve.

## Phase 4 — Materials, procurement and production
- Material catalog, stock visibility, reservation and shortage calculation.
- Configurable production-route/operation templates by product type; retain a shared scheduling, progress and blocker engine.
- Purchase request and receipt workflow.
- Operations, dependencies, capacity calendar, progress logs, blockers and delivery forecast.
**Exit:** project owner can explain forecast from recorded blockers/events.

## Phase 5 — Compliance, quality and release
- Versioned requirement sources and applicability profiles.
- Bind QC, inspection, compliance and release templates to the project/unit product profile; allow justified manual/custom evidence capture.
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
- Deepen and expand the prebuilt template library, integrations and specialized automation based on customer evidence; this phase does not introduce support for additional body types because all types are already in launch scope.
- Customer portal with granular sharing.
- WhatsApp/email integrations.
- OEM templates/partner and government portal integration only when official support is validated.
- Advanced MRP/capacity optimization, CAD workflows, analytics and e-tax integration.

## Test/release gates
- Each migration applies cleanly to empty test DB and is reviewed.
- RLS proves cross-tenant reads/writes denied.
- Storage tests cover upload/download/version/expiry/revocation.
- Workflow tests cover draft/review/approve/supersede/reject.
- Universal product tests prove the same platform can create and run projects for materially different body families and a tenant-defined custom type, including mixed product types in one project.
- Template tests prove version immutability, explicit adoption/revision, custom fallback, and no change to an approved project when a template is updated.
- Critical calculations (BOM, costs, balances, schedule) have deterministic tests.
- AI extraction schema/source citation/untrusted document injection/human approval tests.
- E2E project lifecycle tests on mobile and desktop.
- No release with critical security, data integrity, backup or compliance blockers.

## Work management
Create small issues linked to PRD requirement IDs. Use short-lived feature branches and PRs. Migrations additive and ordered. No broad direct pushes to production branch for application features. Each PR includes tests, migration impact, security considerations and UI screenshots where applicable.

## Dependencies and risks
- A first GTM segment may inform the initial pilot, but it must not determine the product architecture or restrict the supported body types.
- Template coverage will vary by maturity; generic/custom configuration must preserve full common-lifecycle support for types without prebuilt templates.
- Parsing quality and AI cost may constrain the feature set.
- Regulatory source maintenance needs a named owner.
- Cloudflare product/domain configuration follows repository stack inspection.
- Tax treatment for individual business vs future PT and PKP status must be rechecked before billing launch.
- Rp1m net target at Rp1.12m final price must be modeled against actual taxes/payment fees; do not guarantee until verified.
