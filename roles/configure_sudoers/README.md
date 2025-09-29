# Configure Sudoers Role

This role configures sudo privileges for automation users, enabling passwordless sudo access.

---

## Requirements
* Ubuntu/Debian-based system
* Sudo package installed

---

## Role Variables
- None (uses static file `automation-ansible` for sudo configuration).

---

## Dependencies
- None

---

## Example Playbook
```yaml
- hosts: all
  roles:
    - configure_sudoers
  tags:
    - sudoers_configure
```

---

## Notes
- Places `automation-ansible` file in `/etc/sudoers.d/` with validated sudo configuration.
- Ensure `ansible_user` is created by the `configure_users` role before applying.

---

## Idempotency
The role is idempotent. It applies a templated sudoers file with fixed permissions and validates it using `visudo`, ensuring consistent configuration without duplicate entries across multiple executions.