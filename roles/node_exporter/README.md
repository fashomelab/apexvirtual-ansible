# Node Exporter Role

This role installs and configures Prometheus Node Exporter for system metrics collection.

---

## Requirements
* Ubuntu/Debian-based system
* Prometheus server at `10.0.0.20:9090` (or your endpoint)

---

## Role Variables
Available in `defaults/main.yml`:
- `node_exporter_version`: Version to install (e.g., `v1.9.1`).
- `node_exporter_port`: Listening port (e.g., `9100`).

---

## Dependencies
- `prometheus` role (for scraping metrics)

---

## Example Playbook
```yaml
- hosts: all
  roles:
    - node_exporter
  tags:
    - node_exporter_configure
```

---

## Notes
- Installs Node Exporter as a service.
- Update `node_exporter_port` if needed.
- Includes a health check to verify the service is accessible via HTTP after deployment.

---

## Idempotency
The role is idempotent. It deploys Node Exporter via Docker with `state: started`, ensuring the container runs consistently without redundant pulls or restarts on subsequent executions.