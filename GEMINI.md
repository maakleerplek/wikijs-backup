# Maakleerplek Wiki (High Tech Lab)

This repository contains the Markdown-based documentation for the **High Tech Lab (HTL)** at Maakleerplek vzw. It is structured for use with **Wiki.js** and organized by target audience roles.

## Core Mandate: Wiki vs. SharePoint
- **Wiki**: Public information for visitors, technical machine guides/maintenance for volunteers, and IT infrastructure documentation.
- **SharePoint**: Administrative, financial, and organizational data (meeting notes, budgets, legal). **Do not store administrative data in this wiki.**

## Directory Structure

### 1. `/visitors/` (Public)
Publicly accessible information for anyone visiting the lab.
- `home.md`: Landing page.
- `hightechlab.md`: Overview of the lab.
- `machines.md`: Index of available equipment.
- `prices.md`, `schedule.md`, `faq.md`: Operational details.

### 2. `/volunteers/` (Internal Technical)
Maintenance and operational guides for lab volunteers.
- `/volunteers/machines/`: Detailed specs, maintenance logs, and troubleshooting for each machine.
- `stock-system.md`: Instructions for using the InvenTree stock app.
- `closing-checklist.md`, `open-labs.md`: Shift and safety procedures.
- `htl-passwords.md`: Shared passwords for lab equipment (Volunteer access only).

### 3. `/it/` (Private IT)
Technical documentation for the lab's digital services.
- `soteria-doc.md`: Docker infrastructure and deployment guides.
- `htl-temp-server.md`: Local server configuration.
- `kiosk-screen.md`: Dashboard and info screen documentation.
- **Access**: To contribute here, you must be part of the [maakleerplek IT GitHub Team](https://github.com/orgs/maakleerplek/teams/it).

### 4. `/assets/`
Consolidated media (images, icons, svgs) used across all pages.

## Conventions
- **Markdown**: All pages must include YAML frontmatter.
- **Links**: Navigation links in Wiki.js use the folder path (e.g., `/visitors/machines`). 
- **Assets**: Reference images from the root `/assets/` folder.
