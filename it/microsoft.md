---
title: Microsoft Environment
description: Microsoft 365 configuration for Maakleerplek — SharePoint, Teams, Entra ID.
published: true
date: 2026-06-01T05:43:36.266Z
tags: 
editor: markdown
dateCreated: 2026-06-01T05:43:36.266Z
---

# Microsoft Environment

Microsoft 365 configuration for Maakleerplek.

---

## Overview

| Service | URL | Purpose |
|---------|-----|---------|
| **SharePoint** | [maakleerplek.sharepoint.com](https://maakleerplek.sharepoint.com) | Documents, organizational pages |
| **Teams** | Microsoft Teams app | Communication |
| **Entra ID** | [entra.microsoft.com](https://entra.microsoft.com) | Identity management |
| **Outlook** | outlook.office.com | Email |

---

## SharePoint Sites

### High Tech Lab Site

**URL**: [maakleerplek.sharepoint.com/sites/HighTechLab](https://maakleerplek.sharepoint.com/sites/HighTechLab)

| Page | URL |
|------|-----|
| Home | [Home.aspx](https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/Home.aspx) |
| Volunteering | [Volunteering-at-HTL.aspx](https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/Volunteering-at-HTL.aspx) |
| The Lab | [The-HTL-Lab.aspx](https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/The-HTL-Lab.aspx) |
| Open Labs | [Open-Labs.aspx](https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/Open-Labs.aspx) |
| Workshops | [Workshops.aspx](https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/Workshops.aspx) |
| Teams | [Teams.aspx](https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/Teams.aspx) |
| Purchase Rules | [Purchase-rules.aspx](https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/Purchase-rules.aspx) |
| FAQ | [Frequently-Asked-Questions.aspx](https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/Frequently-Asked-Questions.aspx) |
| ICT Info | [HTL-ICT-Info-page.aspx](https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/HTL-ICT-Info-page.aspx) |
| Stock Management | [Stock-management-info-page.aspx](https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/Stock-management-info-page.aspx) |
| All Machines | [All-machines-info.aspx](https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/All-machines-info.aspx) |
| Service Learning | [ServiceLearning.aspx](https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/ServiceLearning.aspx) |
| Student Deadline Days | [Student-Deadline-Days.aspx](https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/Student-Deadline-Days.aspx) |
| Mini Companies | [Mini-companies.aspx](https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/Mini-companies.aspx) |
| Finance Backoffice | [Finance-Backoffice.aspx](https://maakleerplek.sharepoint.com/sites/HighTechLab/SitePages/Finance-Backoffice.aspx) |

### Document Libraries

| Library | URL | Content |
|---------|-----|---------|
| Shared Documents | [All Documents](https://maakleerplek.sharepoint.com/sites/HighTechLab/Shared%20Documents/Forms/AllItems.aspx) | All files |
| Administration | `/Shared Documents/Administration` | Meeting notes, action lists |
| Machines | `/Shared Documents/Machines` | Manuals, maintenance docs |
| Workshops | `/Shared Documents/Workshops` | Workshop materials |
| Communications | `/Shared Documents/Communications` | Templates, logos |

---

## Entra ID

### User Management

Users are created and managed in Microsoft Entra ID (formerly Azure AD).

| User Type | Access |
|-----------|--------|
| Volunteer | SharePoint, Teams |
| IT Team | + Admin access |
| Board | + Financial access |

### Groups

TBD — Document security groups and their purposes.

### Integration with Authentik (Planned)

Entra ID will sync with Authentik to provide SSO for self-hosted services:

```
Entra ID (source of truth)
    ↓ sync
Authentik (SSO for self-hosted)
    ↓ OIDC
Wiki.js, Portainer, InvenTree, etc.
```

---

## Teams

### Channels

TBD — Document Teams structure.

---

## Administration

### Adding Users

1. Create user in Entra ID
2. Assign to appropriate groups
3. User receives welcome email

### Removing Users

1. Disable user in Entra ID
2. Remove from groups
3. Transfer ownership of files if needed

### Permissions

TBD — Document SharePoint permission levels.

---

## See Also

- [User Management](/it/user-management)
- [Authentik](/it/services/authentik)
- [IT Infrastructure](/it)