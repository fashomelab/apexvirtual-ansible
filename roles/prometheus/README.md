# Prometheus Role

This role deploys and configures Prometheus for monitoring, including node-exporter and federation endpoints for apexvirtual hosts.

---

## Requirements
* Ubuntu/Debian-based system
* Docker or direct Prometheus installation
* Access to `192.168.30.200:9090"` and `192.168.40.200:9090"` (or your Prometheus endpoints)

---

## Role Variables
Available in `inventory/apexvirtual/group_vars/all.yml`:
- `prometheus_version`: Version to install (e.g., `v3.3.1`).
- `kubehn_prometheus_endpoint`: Primary Prometheus endpoint (e.g., `http://192.168.30.200:9090"`).
- `kubezd_prometheus_endpoint`: Secondary endpoint (e.g., `http://192.168.40.200:9090"`).

---

## Dependencies
- None (assumes hosts are defined in inventory)

---

## Example Playbook
```yaml
- hosts: monitoring
  roles:
    - prometheus
  tags:
    - prometheus_configure
```

---

## Notes
- Configures `prometheus.yml` via `roles/prometheus/templates/prometheus.yml.j2`.
- Replace `10.0.0.x` IPs with your monitoring endpoints.
- Includes a health check to verify the service is accessible via HTTP after deployment.
--- 

## Idempotency
Fully idempotent. The role deploys Prometheus via Docker with `state: started` and applies a templated `prometheus.yml`, ensuring consistent configuration without redundant changes.