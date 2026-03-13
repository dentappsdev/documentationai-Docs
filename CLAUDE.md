# ChairPulse Documentation — Claude Code Instructions

## Product Context

**ChairPulse** is a dental equipment management and compliance platform. It helps dental practices track equipment, manage compliance requirements, schedule maintenance, troubleshoot issues with AI diagnostics, create SOPs, and manage training paths.

### Source of Truth

The ChairPulse application codebase is located at `/Users/prabesh/projects/chairpulse_main/`. This is read-only reference material. NEVER modify files in that directory. All documentation files live in THIS repo.

### Key Application Facts

**Sidebar Navigation (what users see):**
- Main: Dashboard, Equipment, Issues, Maintenance, Checklists, Compliance, Knowledge, Invoice Analytics, Reports
- Settings (collapsible): Rooms & Locations, Office Settings, Organization (admin/DSO admin only)

**User Roles:** `super_admin`, `admin`, `manager`, `staff`
- Admins and DSO admins see Organization Settings
- Super admins get a separate admin sidebar

**Subscription Tiers:**
- Essential ($99/mo, $82/mo annual): 15 diagnostic chats/mo, 5 reports/mo, 25 SOP generations/mo, max 5 team members. No compliance wizard, no learning paths, no invoice uploads.
- Professional ($139/mo, $115/mo annual): Unlimited diagnostic chats, 30 reports/mo, unlimited SOP generation, max 25 team members. Full access to compliance wizard, learning paths, detailed SOPs, invoice uploads.
- Trial: Same limits as Professional.

**Equipment Categories (30):** 3D Printers, Air Polishers, Amalgam Separators, Amalgamators, Apex Locators, Autoclaves & Sterilizers, Compressors, Curing Lights, Dental Chairs & Delivery Units, Dental Lasers, Dental Microscopes, Digital Scanners & CAD/CAM, Electric Handpiece Motors, Electrosurgery Units, Endodontic Equipment, Handpieces, Implant Motors, Intraoral Cameras, Lab Equipment, Mixing Machines, Nitrous Oxide Systems, Operatory Lights, Patient Monitors, Prophy Jets, Suction Units, Ultrasonic Cleaners, Ultrasonic Scalers, Vacuum Systems, X-Ray & Imaging, Other.

**Room Types (9):** Operatory, Sterilization, Lab, X-Ray Room, Mechanical Room, Storage, Reception, Office, Other.

**Compliance Categories (8):** Radiation Equipment, Sterilization Equipment, Sedation Systems, Water Systems, Air & Vacuum Systems, Safety Equipment, Waste Management, Other.

**Compliance Primitives (6):**
- `inspector` — "Pass / Fail Inspection" — Record a pass or fail result
- `meter` — "Numeric Reading" — Record a measurement checked against a threshold
- `clock` — "Expiration Tracker" — Confirm expiration date
- `auto` — "Auto-Tracked" — Automatically managed, no action needed
- `heartbeat` — "Confirmation" — Simple check-off
- `certificate` — "Certificate Upload" — Upload certificate or proof

**Task Statuses:** pending, in_progress, completed, completed_with_failure, overdue, skipped, awaiting_result, missed

**Task Frequencies:** daily, weekly, monthly, quarterly, semi_annual, annual, one_time, biennial, triennial, every_3_years, every_4_years, every_5_years, as_needed

---

## Writing Style

- Write for dental office managers and staff, not engineers
- Use exact UI labels from the codebase (button text, field names, menu items)
- Use dental-specific examples (autoclave spore testing, X-ray registration, OSHA training)
- Always include expected outcomes after action steps
- Note tier restrictions with a Callout when a feature is Professional-only
- Cross-link aggressively between related pages
- Add `<!-- REVIEW: description -->` comments where uncertain about UI details

---

## Documentation.ai Component Reference

### Frontmatter (required)
```
---
title: "Page Title"
description: "Brief description for SEO and previews"
---
```

### Headings
- Body content starts at `##` (H2) — never use H1
- H1 is auto-generated from the frontmatter title

### Steps (sequential procedures)
```mdx
<Steps>
  <Step title="Step title">
    Step content here.
  </Step>
  <Step title="Next step">
    More content.
  </Step>
</Steps>
```
Do NOT use numbered markdown lists for procedures.

### Callouts
```mdx
<Callout kind="info" title="Optional title">
  Content here.
</Callout>
```
Kinds: `info`, `tip`, `alert`, `danger`, `success`

### Expandable / ExpandableGroup
```mdx
<ExpandableGroup>
  <Expandable title="Question here?">
    Answer content.
  </Expandable>
  <Expandable title="Another question?">
    Another answer.
  </Expandable>
</ExpandableGroup>
```

### Tabs
```mdx
<Tabs>
  <Tab title="Tab One">
    Content for tab one.
  </Tab>
  <Tab title="Tab Two">
    Content for tab two.
  </Tab>
</Tabs>
```

### Cards in Columns
```mdx
<Columns>
  <Card title="Card Title" icon="icon-name" href="/section/page">
    Brief description.
  </Card>
  <Card title="Another Card" icon="icon-name" href="/section/page">
    Brief description.
  </Card>
</Columns>
```

### Internal Links
Use absolute paths: `[link text](/section/page-name)` — never relative paths.

### Images
Use placeholder comments: `<!-- Screenshot needed: description of what to capture -->`

---

## Page Generation Rules

1. Every file starts with `---` frontmatter containing `title` and `description`
2. Body content starts at `##` (H2)
3. Use `<Steps>` for sequential procedures
4. Use `<Callout>` for important notes
5. Use `<Expandable>` / `<ExpandableGroup>` for FAQ content
6. Use `<Tabs>` for role-specific or tier-specific content
7. Use `<Columns>` with `<Card>` for navigation grids
8. Internal links use absolute paths
9. All multi-word attributes use kebab-case
10. Image placeholders: `<!-- Screenshot needed: description -->`

---

## Codebase Reference Map

| Doc Section | Source Files |
|---|---|
| Dashboard | `src/pages/Dashboard.tsx`, `src/components/dashboard/` |
| Equipment | `src/pages/Equipment.tsx`, `src/pages/EquipmentNew.tsx`, `src/pages/EquipmentDetail.tsx`, `src/components/equipment/` |
| Rooms | `src/pages/Rooms.tsx`, `src/components/rooms/`, `src/lib/roomTypes.ts` |
| Compliance | `src/pages/Compliance.tsx`, `src/components/compliance/`, `src/lib/compliance-engine/` |
| Maintenance | `src/pages/Maintenance.tsx`, `src/components/maintenance/` |
| Issues | `src/pages/Issues.tsx`, `src/pages/IssueNew.tsx`, `src/pages/IssueDetail.tsx`, `src/components/issues/` |
| Diagnostics | `src/pages/DiagnosticChat.tsx`, `src/pages/DiagnosticReportPage.tsx`, `src/components/diagnostic/` |
| Knowledge/SOPs | `src/pages/Knowledge.tsx`, `src/pages/Sops.tsx`, `src/pages/SopCreate.tsx`, `src/components/sops/` |
| Training Paths | `src/pages/LearningPaths.tsx`, `src/pages/LearningPathDetail.tsx`, `src/components/learning-paths/` |
| Invoices | `src/pages/InvoiceAnalytics.tsx`, `src/components/invoices/` |
| Checklists | `src/pages/Checklists.tsx`, `src/components/checklists/` |
| Settings | `src/pages/OfficeSettings.tsx`, `src/pages/OrganizationSettings.tsx`, `src/components/settings/` |
| Reports | `src/pages/Reports.tsx`, `src/components/reports/` |
