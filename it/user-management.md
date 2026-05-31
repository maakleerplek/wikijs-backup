---
title: User Management
description: User account management — Authentik SSO and Ansible server accounts.
published: true
date: 2026-05-31T21:00:00.000Z
tags: it, users, sso, ansible
editor: markdown
dateCreated: 2026-05-31T21:00:00.000Z
---

# User Management

User accounts at Maakleerplek are managed through two systems:

1. **Authentik SSO** — Single sign-on for web services
2. **Ansible** — Server user accounts and SSH keys

---

## Authentik SSO

> Authentik is planned but not yet deployed.
{.is-warning}

Authentik will provide single sign-on for all Maakleerplek web services.

### Planned Features

- Single login for Wiki.js, Portainer, InvenTree, etc.
- Integration with Microsoft Entra ID
- Automatic user provisioning
- MFA support

### User Lifecycle (Planned)

| Event | Action |
|-------|--------|
| New volunteer | Created in Entra ID → synced to Authentik |
| Access request | Admin assigns application in Authentik |
| Volunteer leaves | Disabled in Entra ID → synced to Authentik |

### Connected Services (Planned)

| Service | Protocol |
|---------|----------|
| Wiki.js | OIDC |
| Portainer | OIDC |
| InvenTree | OIDC |
| Stock Frontend | OIDC |

See [Authentik service page](/it/services/authentik) for technical details.

---

## Ansible Server Accounts

Server user accounts (SSH access) are managed via Ansible.

### Repository

TBD — Ansible playbooks for user management.

### How It Works

1. User SSH public key added to Ansible inventory
2. Playbook run to deploy keys to servers
3. User can SSH to servers with their key

### Adding a User

```yaml
# In ansible inventory (example)
users:
  - name: username
    groups: [sudo, docker]
    ssh_keys:
      - "ssh-ed25519 AAAA... user@machine"
```

Run playbook:
```bash
ansible-playbook -i inventory users.yml
```

### Removing a User

1. Remove user from Ansible inventory
2. Run playbook with `state: absent`

### Servers Managed

| Server | SSH Access |
|--------|------------|
| [Soteria](/it/servers/soteria) | Yes |
| [HTL Temp Server](/it/servers/htl-temp-server) | Yes |
| [Kiosk Pi](/it/servers/kiosk-pi) | Yes |

---

## Access Levels

| Level | Authentik | Server SSH | Description |
|-------|-----------|------------|-------------|
| **Volunteer** | App access | No | Can use web services |
| **IT Team** | Admin access | Yes | Can manage services and servers |
| **Admin** | Full access | sudo | Full system access |

---

## See Also

- [Authentik](/it/services/authentik)
- [Microsoft Environment](/it/microsoft)
- [IT Infrastructure](/it)
