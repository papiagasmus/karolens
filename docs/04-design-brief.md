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
