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
