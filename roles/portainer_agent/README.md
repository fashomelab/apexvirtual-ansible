# Portainer Agent Role

This role deploys the Portainer Agent for managing Docker containers remotely.

---

## Requirements
- Ubuntu/Debian-based system
- Docker installed
- Portainer server running

---

## Role Variables
Available in `defaults/main.yml`:
- `portainer_agent_version`: Version to install (e.g., `2.20.0`).
- `portainer_server_url`: Portainer server URL (e.g., `http://10.0.0.10:9000`).

---

## Dependencies
- `docker` role

---

## Example Playbook
```yaml
- hosts: docker_hosts
  roles:
    - portainer_agent
  tags:
    - portainer_configure
```
---

## Notes
- Deploys Portainer Agent as a Docker container.
- Update `portainer_server_url` with your Portainer server.

---

## Idempotency
Idempotent and efficient. The role deploys the Portainer Agent via Docker with `state: started`, applying changes only if the container is not already correctly configured.