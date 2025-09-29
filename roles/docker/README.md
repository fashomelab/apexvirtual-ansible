# Docker Role

This role installs and configures Docker for running containerized services in the apexvirtual.

---

## Requirements
* Ubuntu/Debian-based system
* Internet access for Docker repository

---

## Role Variables
Available in `defaults/main.yml`:
- `docker_version`: Docker version to install (default: `latest`).
- `docker_users`: List of users to add to the `docker` group (default: `["ansible_user"]`).

---

## Dependencies
- None

---

## Example Playbook
```yaml
- hosts: docker_hosts
  roles:
    - docker
  tags:
    - docker_configure
```

---

## Notes
- Installs Docker CE and Docker Compose.
- Ensure `ansible_user` has sudo privileges for installation.

---

## Idempotency
The role is idempotent. It installs Docker and manages group membership with `state: present`, checking existing packages and services to prevent redundant modifications on re-runs.