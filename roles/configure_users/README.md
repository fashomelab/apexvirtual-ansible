# Configure Users Role

This role creates and manages user accounts on target hosts, including SSH key setup and sudo privileges for automation users.

---

## Requirements
* Ubuntu/Debian-based system
* HashiCorp Vault for user credentials and SSH keys

---

## Role Variables
- `ansible_user`: Automation user (default: `ansible_user`).
- `user_ssh_keys`: SSH public keys from Vault (e.g., `kv/data/apexvirtual/ansible-credentials/ssh_keys`).
- `user_password`: Hashed password from Vault (e.g., `kv/data/apexvirtual/ansible-credentials/password`).

---

## Dependencies
- Vault path: `kv/data/apexvirtual/ansible-credentials/*`
- `configure_sudoers` role (for sudo privileges)

---

## Example Playbook
```yaml
- hosts: all
  roles:
    - configure_users
  tags:
    - users_configure
```
---

## Notes
- Configures `ansible_user` with passwordless sudo (via `configure_sudoers`).
- Update Vault paths with your user credentials and SSH keys.

---

## Idempotency
Fully idempotent. The role uses `state: present` for user creation and SSH key setup, applying changes only when necessary to avoid duplicate users or authorized keys.