# Server Provision Role

This role provisions new servers, setting up initial configurations like hostname, timezone, and base packages.

---

## Requirements
- Ubuntu/Debian-based system
- Proxmox API access (via `inventory/apexvirtual/inventory.proxmox.yml`)

---

## Role Variables
- `server_hostname`: Hostname to set (e.g., `{{ inventory_hostname }}`).
- `server_timezone`: Timezone (e.g., `UTC`).
- `base_packages`: List of packages to install (e.g., `["curl", "vim"]`).

---

## Dependencies
- Vault path: `kv/data/apexvirtual/proxmox-credentials`

---

## Example Playbook
```yaml
- hosts: new_servers
  roles:
    - server_provision
  tags:
    - provision
```

---

## Notes
- Sets up new VMs via Proxmox or bare-metal servers.
- Update `server_hostname` and `base_packages` as needed.

---

## Idempotency
The role is idempotent. It installs packages with `state: present`, ensuring only missing packages are added, preventing duplicates on repeated runs.