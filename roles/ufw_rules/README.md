# UFW Rules Role

This role configures Uncomplicated Firewall (UFW) rules to secure apexvirtual hosts.

---

## Requirements
- Ubuntu-based system
- UFW package installed
- HashiCorp Vault for firewall rules

---

## Role Variables
- `ufw_rules_from_vault`: Firewall rules from Vault (e.g., `kv/data/apexvirtual/ansible-config/ufw-rules`).

---

## Dependencies
- Vault path: `kv/data/apexvirtual/ansible-config/ufw-rules`

---

## Example Playbook
```yaml
- hosts: all
  roles:
    - ufw_rules
  tags:
    - ufw_configure
```

---

## Notes
- Enables UFW and sets rules for common ports (e.g., SSH, HTTP).
- Update Vault path for your network-specific rules.
- The role ensures UFW is both running (`state: started`) and enabled on boot (`enabled: true`) after applying firewall rules.

---

## Idempotency
Idempotent and secure. The role installs UFW and applies firewall rules with `state: present` and `state: enabled`, ensuring rules are only added if not already present.