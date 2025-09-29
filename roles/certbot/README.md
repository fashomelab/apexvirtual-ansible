# Certbot Role

This role manages SSL certificates using Certbot with the Cloudflare DNS plugin for services like Nginx.

---

## Requirements

* Ubuntu/Debian-based system
* **Snapd** installed for the Certbot snap package.
* HashiCorp Vault with a valid Cloudflare API token.

---

## Role Variables

Variables are available in `inventory/av-onprem/group_vars/reverse_proxy.yml`:

* **`cert_primary_domain`**: The primary domain for the certificate (e.g., `example.local`).
* **`cert_alt_names`**: A list of alternative SANs for the certificate (e.g., `["*.example.local"]`).
* **`cert_email`**: The admin email for Let's Encrypt notifications (e.g., `admin@example.com`).

---

## Tasks Performed

* Uninstalls any existing `apt` versions of Certbot to avoid conflicts.
* Installs the official Certbot snap package.
* Installs the Cloudflare DNS plugin via Snap.
* Retrieves the Cloudflare API token securely from HashiCorp Vault.
* Places the token in `/etc/letsencrypt/cloudflare.ini` with secure permissions (`0400`).
* Requests a Let's Encrypt certificate for the specified domains.
* Creates a renewal hook to automatically reload Nginx when certificates are renewed.

---

## Dependencies

* **Vault Path**: `kv/data/apexvirtual/ansible-credentials/cloudflare` (for the API token).
* **`nginx` role**: This role must be applied to the host to configure Nginx for SSL termination.

---

## Example Playbook

```yaml
- hosts: reverse_proxy
  roles:
    - certbot
  tags:
    - certs
```
---

## Notes
- This role is designed to run after the nginx role has been configured on the target host.
- The Cloudflare API token is stored securely in /etc/letsencrypt/cloudflare.ini and is never logged.

---
## Idempotency
This role is idempotent. It uses the `creates` parameter in the Certbot command to avoid redundant certificate requests and employs `state: present` for package and snap installations, ensuring no unnecessary changes on subsequent runs.