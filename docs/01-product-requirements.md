# 01 — Product Requirements Document (PRD)

## Document control
- Product: Karolens
- Version: 1.0-draft
- Date: 2026-11-07
- Status: Draft for product review; not implementation approval
- Related: TRD, App Flow, Design Brief, Backend Schema, Implementation Plan

## 1. Product vision
Karolens is a project operating system for Indonesian vehicle-body manufacturers (karoseri). It connects customer requirements, technical knowledge, contract obligations, material planning, production, regulatory evidence, customer communications, billing, delivery, and warranty in one traceable project record.

**Positioning:** The Karoseri Project & Compliance Operating System.

**Value promise:** From customer specification to a compliant, profitable vehicle delivery.

## 2. Commercial baseline
- Customer-facing target price: **Rp1.120.000 per company per month**, one final price; do not add a separate tax line to the advertised price in the product's pricing presentation.
- Internal net-receipt target: Rp1.000.000 per company per month after applicable taxes and fees. This is a planning goal, not a tax conclusion or guaranteed result. Accounting must model the actual individual-business and later PT tax status, VAT/PKP obligations, payment fees, and withholding treatment before launch. Do not encode a flat tax assumption as universal law.
- Pricing unit is a customer company/workspace, not per user, unless a future pricing decision changes it.

## 3. Target users and jobs
Primary customer: Indonesian karoseri company, initially SMEs/medium-size operators where project coordination is fragmented across spreadsheets, paper, chat, and separate systems.

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
- Evidence before status: status changes require attributable records.
- Human approval for technical baselines, contractual interpretation, legal/compliance sign-off, and customer-facing reports.
- Distinguish law/regulation, OEM requirements, customer contract clauses, and internal SOP.
- Do not claim to issue government approvals or replace Kemenhub portals.
- Mobile-first shop-floor experience; full desktop capability for planning, finance, and document control.
- Tenant isolation by company; auditability by default.

## 5. Core domains
1. Commercial & Project Management: customers, quotations, orders, project creation, milestones, ownership, status.
2. Project Knowledge & Document Intelligence: uploads, versioning, extraction, citations, annotations, verification, project knowledge retrieval.
3. Contract & Obligation Management: clauses, obligations, payment schedule, delivery deadlines, warranty, penalties, acceptance, variation/change orders.
4. Engineering & Technical Intelligence: specification baseline, drawing revisions, vehicle/unit configuration, BOM, change-impact assessment.
5. Material & Production Control: material availability, purchasing requests, goods receipt, inventory allocation, production work orders, progress, dependencies, capacity and forecast.
6. Regulatory & Company Compliance: company-level permits/reporting evidence and per-unit regulatory dossier tracking.
7. Quality & Vehicle Release: inspection plans/checklists, nonconformities, rework, calibration evidence, release gates.
8. Customer Reporting & Communication: verified project reports, communication log, approved shareable documents, later customer portal.
9. Billing & Receivables: milestone invoices, due dates, payments, allocation, outstanding balances and reminders.
10. Delivery & After-Sales: handover dossier, delivery confirmation, warranty terms and claims.

## 6. Project workspace and uploaded knowledge
Supported initial uploads: PDF, common images, DOCX, XLSX, and other validated office formats. File size/type limits are configuration decisions. Native CAD parsing is out of MVP unless separately proven; accept PDF/image exports initially.

Each file has immutable versions, uploader, timestamp, source, checksum, project association, visibility, and review state. AI may extract text/tables/fields, summarize, identify entities, compare versions, identify potential inconsistencies, and answer project questions with citations to source file/version/page or image region where supported.

Knowledge states:
- Uploaded — stored, not analyzed.
- Extracted — machine-extracted candidate facts.
- Verified — reviewed by an authorized person.
- Approved/Baseline — formally approved source of truth.

AI-extracted information must never silently become the approved engineering specification, contract baseline, or compliance pass. Every consequential fact must retain lineage to the source and reviewer action.

## 7. Contract obligations
Capture, with human review: scope, specifications, price, payment terms, advance/progress/final milestones, delivery deadline, acceptance criteria, penalty/liquidated damages, warranty, exclusions, variation orders, dispute provisions, and signatures/versions. Approved clauses create linked obligations and reminders. AI flags possible risks; it does not provide binding legal advice or modify signed contracts.

## 8. Project planning and execution
A project should link one or more vehicle units, approved configuration/specification, BOM revisions, required materials/components, supplier/procurement records, production operations, dependencies, capacity, start/finish dates, risks, and progress evidence.

Planning must expose assumptions and confidence. Delivery forecast should show expected date plus drivers/blockers (material, engineering approval, capacity, rework, inspection, documentation, customer dependency). Avoid false precision when source data is incomplete.

## 9. Regulatory and release management
Track applicability and evidence, not generic checklists detached from context. Requirements are classified by jurisdiction and source type: mandatory national/local regulation, OEM certification/requirement, customer contract, and company SOP. Each requirement records source, effective date/version, applicability rule, owner, required evidence, due date, verification status, and reviewer.

Karolens may prepare/checklist/track SKRB, SUT, physical test/BAP, SRUT and supporting evidence according to applicable workflows; it does not submit or issue legal approvals unless an officially supported integration is separately validated. Keep per-vehicle identity and dossier linkage. Owner/authorized party responsibility for vehicle registration steps must be configurable by contract and legal context.

## 10. Customer reports and billing
Reports: periodic progress, schedule/forecast, blockers, approved photos, milestone completion, inspection, delivery and warranty. Customer output must exclude internal margin, supplier costs, internal risk notes, and restricted data unless explicitly approved.

Billing supports commercial invoices and milestone receivables. Clearly distinguish a commercial invoice from a tax invoice (Faktur Pajak). E-tax integration is not MVP. Support partial payments, allocations, overdue tracking, payment evidence, and audit history.

## 11. MVP scope
MVP must demonstrate the connected workflow on one selected karoseri subsegment and one representative project template:
- company workspace, users, roles, customers, projects and units;
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

Explicitly out of initial MVP: full accounting/GL, payroll, automatic legal judgement, direct government approval issuance, full CAD/BIM engine, supplier marketplace, customer self-service portal (can be Phase 2), complex MRP optimizer, and unsupervised AI actions.

## 12. Non-functional requirements
Security: tenant isolation, least privilege, RLS on exposed tables, private file buckets, signed access, audit trails, secure secrets. Reliability: backups/recovery plan, idempotent background processing, observable jobs. Performance: mobile-usable common screens; pagination and async document processing. Accessibility: readable contrast, keyboard operation on desktop, clear status semantics. Data portability: exports of project data and documents with metadata.

## 13. Success metrics
Activation: first customer/project created, first file uploaded and verified, first obligation/schedule established. Workflow: percentage of projects with approved baseline, BOM completeness, material shortage visibility, milestone reporting cadence, inspection evidence completeness, overdue receivables visibility. Outcomes: on-time delivery trend, rework trend, estimate-vs-actual variance, collection delay, time spent preparing customer reports. Do not claim outcome improvements until measured with real product data.

## 14. Risks and assumptions
- Karoseri workflows vary by body type, OEM, customer, and project complexity.
- Existing solutions (karoseri ERP, Odoo/custom ERP, OEM PDI) mean generic ERP/QC is not enough differentiation.
- Rp1.120.000 pricing and net Rp1.000.000 economics remain hypotheses, not proven WTP.
- Legal requirements change and depend on vehicle category, company scale/risk, process and location.
- AI extraction may misread technical tables/drawings; approval gate and citations are mandatory.
- Customer willingness to centralize contracts and drawings depends on trust, privacy, and usability.

## 15. Acceptance criteria for PRD approval
- First target subsegment and representative workflow explicitly selected.
- MVP boundaries approved by product owner.
- Roles and critical approval matrix agreed.
- Legal requirement source registry owner and update cadence assigned.
- Commercial model and price/tax handling reviewed by accountant.
- Each MVP requirement mapped to flow, UI, backend tables, and implementation phase.
