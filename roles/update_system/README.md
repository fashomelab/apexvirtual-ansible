# Update System Role

This role updates the system packages and ensures the latest security patches are applied.

---

## Requirements
- Ubuntu/Debian-based system
- Sudo privileges for package management

---

## Role Variables
Available in `defaults/main.yml`:
- `update_cache`: Whether to update apt cache (e.g., `true`).
- `upgrade_type`: Upgrade type (e.g., `dist` for full upgrade).

---

## Dependencies
- None

---

## Example Playbook
```yaml
- hosts: all
  roles:
    - update_system
  tags:
    - update_system
```

---

## Notes
- Updates the package cache and applies full upgrades for Debian-based systems (`apt`).
- Enables the `apt-daily` service to ensure automatic updates are configured.
- Reboots are performed only if required, based on the presence of `/var/run/reboot-required`.

---

## Idempotency
Partially idempotent. The package cache update (`apt update`) runs every time and is marked as changed. Package upgrades (`apt upgrade -y`), `apt-daily` service enablement, and reboots are conditional, only applying when updates are available or a reboot is required (`/var/run/reboot-required` exists).