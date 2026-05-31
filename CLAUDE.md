# Maakleerplek Wiki - Project Guide

Git-based backup of **Maakleerplek** Wiki.js documentation, focused on volunteer technical documentation.

**Repository:** `git@github.com:maakleerplek/wikijs-backup.git`

## Purpose

1. **Technical Documentation** - Volunteer-maintained docs for machines, IT, and operations
2. **Disaster Recovery** - Version-controlled backup of Wiki.js content
3. **Change History** - Git audit trail for documentation changes

## Content Scope

### Wiki (this repo)
- Machine maintenance and technical guides
- IT infrastructure documentation
- Operational procedures (checklists, restocking)
- Stock system technical docs

### SharePoint (not here)
- Organizational info (volunteering, open labs, teams)
- Administrative/financial documents
- Meeting notes, policies
- FAQ, workshops info

**Rule**: If SharePoint has a page for it, link to SharePoint instead of duplicating.

## Directory Structure

```
├── visitors/              # Public info
│   ├── hightechlab.md    # Main landing page
│   ├── machines.md       # Equipment index → links to /volunteers/machines/
│   ├── prices.md         # Pricing
│   └── schedule.md       # Opening hours
│
├── volunteers/            # Volunteer docs
│   ├── volunteer-hub.md  # Central hub with SharePoint links
│   ├── stock-system.md   # Stock system technical docs
│   ├── closing-checklist.md
│   ├── restocking.md
│   ├── htl-passwords.md  # Protected
│   └── machines/         # Per-machine technical docs
│       ├── laser-cutter-big.md
│       ├── 3dp-bambu-*.md
│       └── ...
│
├── it/                    # IT infrastructure
│   ├── index.md          # IT main page
│   ├── user-management.md
│   ├── servers/
│   │   ├── soteria.md        # Main Docker host (full docs)
│   │   ├── helios.md
│   │   ├── htl-temp-server.md
│   │   └── kiosk-pi.md
│   ├── services/
│   │   ├── wikijs.md
│   │   ├── portainer.md
│   │   ├── authentik.md
│   │   ├── inventree.md
│   │   ├── stock-frontend.md
│   │   └── dashboard.md
│   ├── networking/
│   │   └── index.md      # Network topology, VLANs, DNS
│   └── microsoft/
│       └── index.md      # M365, SharePoint, Entra ID
│
└── assets/                # Images, logos
```

## Conventions

### File Naming
- Use hyphens: `laser-cutter-big.md` (not underscores)

### Frontmatter
```yaml
---
title: Page Title
description: Brief description
published: true
date: 2026-05-31T12:00:00.000Z
tags: htl, category
editor: markdown
dateCreated: 2025-01-01T12:00:00.000Z
---
```

### Links
- Internal: `/visitors/machines`
- SharePoint: Full URL
- Assets: `/assets/filename.png`

## Key SharePoint Links

| Page | URL |
|------|-----|
| Volunteering | `https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/Volunteering-at-HTL.aspx` |
| Open Labs | `https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/Open-Labs.aspx` |
| Teams | `https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/Teams.aspx` |
| Workshops | `https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/Workshops.aspx` |
| FAQ | `https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/Frequently-Asked-Questions.aspx` |
| Documents | `https://maakleerplek.sharepoint.com/sites/HighTechLab/Shared%20Documents/Forms/AllItems.aspx` |

## Access Control

- `/visitors/` - Public
- `/volunteers/` - Maakleerplek volunteers
- `/it/` - [Maakleerplek IT Team](https://github.com/orgs/maakleerplek/teams/it)
