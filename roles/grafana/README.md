# Grafana Role

This role deploys and configures Grafana for monitoring dashboards, integrated with Prometheus.

---

## Requirements
* Ubuntu/Debian-based system
* Docker or direct Grafana installation
* Prometheus running at `10.0.0.20:9090` (or your endpoint)
* HashiCorp Vault for admin credentials

---

## Role Variables
Available in `roles/grafana/vars/main.yml`:
- `grafana_version`: Version to install (e.g., `12.0.0`).
- `grafana_prometheus_url`: Prometheus endpoint (e.g., `http://stormbird.lab.apexvirtual.internal:9090`).

---

## Dependencies
- `prometheus` role
- Vault path: `kv/data/apexvirtual/grafana/credentials`

---

## Example Playbook
```yaml
- hosts: monitoring
  roles:
    - grafana
  tags:
    - grafana_configure
```

---

## Notes
- Configures Grafana with Prometheus as a data source.
- Replace `grafana_prometheus_url` with your endpoint.
- Includes a health check to verify the service is accessible via HTTP after deployment.

---

## Idempotency
The role is idempotent. It deploys Grafana via Docker with `state: started` and configures the Prometheus data source with `state: present`, maintaining consistency without unnecessary changes.