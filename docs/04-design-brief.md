# 04 — Design Brief Document

## Document control
- Product: Karolens | Version: 1.0-draft | Date: 2026-11-07

## 1. Design intent
Create a confident, premium industrial operations interface: precise, legible, calm under pressure, and optimized for quick decisions on desktop and mobile. Avoid generic admin-dashboard appearance and excessive decoration.

## 2. Experience principles
- One glance: what is happening, what is blocked, what needs action.
- Evidence-led: status always links to the underlying source, approval, or event.
- Progressive disclosure: summary first, technical detail on demand.
- Consistency: same lifecycle status and severity language across screens.
- Field-ready: large touch targets, readable typography, fast capture, resilient upload flows.
- Finance/engineering accuracy over decorative visuals.

## 3. Visual direction
- Overall: modern industrial control room; premium but practical.
- Typography: Jakarta Sans or equivalent highly legible sans-serif; establish type scale and numeric/tabular styles.
- Palette: neutral graphite/stone foundations with restrained blue/teal primary accent; amber for warning, red for critical, green for verified/complete. Do not rely on color alone; pair with icon/label.
- Surface: clean cards/panels, subtle borders, restrained shadow. Avoid heavy glassmorphism if it harms contrast, rendering or performance.
- Charts: only when they support decisions; show units, period, provenance and drill-down.

## 4. Responsive behavior
- Mobile: primary use is capture/review/approval/status update. Use compact top bar, contextual project switcher, bottom navigation or drawer based on tested information architecture, sticky key actions, touch-friendly forms.
- Tablet: split-pane operational lists and details.
- Desktop: dense planning grids, comparison views, contract/document editing, finance registers and dashboards.
- Never require horizontal scrolling for common mobile tasks; specialized BOM/schedule tables may use controlled responsive alternatives.

## 5. Dashboard information hierarchy
1. Overall portfolio health: active projects, at-risk projects, overdue milestones, material blockers, release-ready units, overdue receivables.
2. Action queue: approvals, procurement shortages, inspections, expiring documents, report approvals, invoices due.
3. Project portfolio: customer, body/unit type, progress, forecast, status and responsible manager.
4. Drill-down to project with evidence and action.

## 6. Project screen
Header: project number/name, customer, unit count, lifecycle status, forecast delivery, project owner. At-a-glance indicators: engineering baseline, materials, production, compliance, QC, customer reporting, billing. Timeline/activity stream records who changed what and why.

## 7. Component system
Define tokens for color, spacing, radius, typography, shadows, focus rings and motion. Components: AppShell, Sidebar/BottomNav, PageHeader, ProjectHeader, StatusBadge, MetricCard, ActionQueue, DataTable, FilterBar, EmptyState, UploadDropzone, FileVersionStack, EvidenceCitation, ApprovalPanel, Timeline, ScheduleBoard, BOMTable, RequirementChecklist, QCResult, InvoiceSummary, ReportPreview, ConfirmDialog, Toast, Command/Quick Search.

## 8. Status and severity grammar
Lifecycle: Draft, Active, On Hold, At Risk, Completed, Cancelled. Review: Uploaded, Processing, Extracted, Needs Review, Verified, Approved/Baseline, Rejected, Superseded. Requirement: Not Applicable (with reason), Missing, In Progress, Submitted/External Review, Approved/Verified, Expired, Rejected. Severity: Info, Warning, Critical. Ensure definitions are centrally governed.

## 9. Interaction and motion
Use subtle, functional transitions for navigation, panel expansion, processing progress and state changes. Respect reduced-motion preferences. Avoid animations that delay data entry or obscure state.

## 10. Accessibility and content
Meet WCAG AA contrast where practicable. Keyboard focus visible. Labels and errors explicit. Use Indonesian as default UI language for initial market; structure for future localization. Use familiar business terminology and explain abbreviations contextually.

## 11. Important screen inventory
Auth and organization setup; dashboard; customer list/detail; project list/detail; project files/knowledge; document compare/review; contract & obligation register; specification editor/version compare; BOM/material availability; schedule/production; procurement; compliance library/register; unit dossier; QC and nonconformity; customer report composer; invoice/receivable; delivery/warranty; member/role/settings.

## 12. UX acceptance checks
A supervisor can record progress/photo on mobile quickly; an engineer can compare drawing revisions and approve facts with source; a manager can identify blockers/forecast reason; finance can see due and received amounts; a report approver can detect confidential data before sharing; a customer viewer cannot navigate to internal data.
