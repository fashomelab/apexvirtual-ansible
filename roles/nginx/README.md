# Nginx Role

This role installs and configures an Nginx reverse proxy server with SSL support, managing site configurations for services like Jellyfin, Vaultwarden, and Proxmox.

---

## Requirements
* Ubuntu/Debian-based system  
* Sudo privileges for package installation  
* Certbot role (for SSL certificates)  
* HashiCorp Vault instance for Cloudflare API token  

---

## Role Variables
Available in `inventory/apexvirtual/group_vars/reverse_proxy.yml`:

```yaml
nginx_sites:
  - name: backup
    server_name: "backup.lab.apexvirtual.internal"
    template: "site.conf.j2"
    proxy_pass_url: "http://192.168.50.134"
    is_websocket: true
  - name: jellyfin
    server_name: "jellyfin.lab.apexvirtual.internal"
    template: "jellyfin.conf.j2"
    proxy_pass_url: "http://jellyfin:8096"
    resolver_ip: "192.168.30.88"
```

---

## Dependencies
- `certbot` role (for SSL termination)
- Vault path: `kv/data/apexvirtual/certbot/cloudflare`

---

## Example Playbook
```yaml
- hosts: proxy
  roles:
    - nginx
  tags:
    - nginx_configure
```

---

## Notes
- Installs Nginx via apt and configures sites using templates in roles/nginx/templates/.
- Update nginx_sites in group_vars/reverse_proxy.yml with your domains and IPs
- All configuration templates are validated with `nginx -t` before deployment to ensure syntax correctness.
- Changes to configurations trigger an Nginx restart via the `Restart nginx` handler.

---

## Idempotency
Idempotent and reliable. The role uses `state: present` for package installation and `state: link` for site configurations, checking existing states to avoid duplicate or conflicting changes.