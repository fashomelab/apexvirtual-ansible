# Fail2Ban Role

This role configures Fail2Ban for intrusion prevention, protecting services like SSH and Nginx.

---

## Requirements
* Ubuntu/Debian-based system
* Fail2Ban package installed
* HashiCorp Vault for ignored IPs and email

---

## Role Variables
- `fail2ban_ignore_ips`: List of IPs to ignore (from `kv/data/apexvirtual/fail2ban/ignore_ips`).
- `fail2ban_email`: Notification email (from `kv/data/apexvirtual/fail2ban/email`).
- `fail2ban_destemail`: Email address for ban notifications (from Vault, default: `admin@example.com`).
- `fail2ban_sender`: Sender email for notifications (from Vault, default: `fail2ban@hostname`).

---

## Dependencies
- Vault path: `kv/data/apexvirtual/fail2ban/*`

---

## Example Playbook
```yaml
- hosts: all
  roles:
    - fail2ban
  tags:
    - fail2ban_configure
```

---

## Notes
- Configures jails for common services (e.g., SSH, Nginx).
- Update Vault paths for your setup.
- Email notifications are enabled by default using Vault-stored addresses. Override in Vault path `kv/data/apexvirtual/ansible-config/fail2ban`.

---

## Idempotency
Idempotent by design. The role uses `state: present` for package installation and templates for configuration files, ensuring only required changes are applied without redundant jail setups.