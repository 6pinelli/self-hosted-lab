### self-hosted-lab
Documentation of the creation, monitoring and troubleshooting of a self-hosting lab infrastructure
built as part of the "Infrastructure Lab Workshop".
This will include using Open Source Services, Linux and Docker.

## Services to be used
Function             | Service used                         | Functional Description
| :--- | :--- | :--- |
As foundation        | Ubuntu Server VM through Virtual Box | Industry Standard Desktop less Server   
Container runtime    | Docker and Docker Compose            | Hosting services below  
DNS/Ad-blocking      | Pi-hole                              | DNS filtering, log visibility  
Files/Photo backup   | File Browser, Immich                | Volumes, persistant storage, Multi-container, databases
Password Management  | Vaultwarden                          | Secrets, HTTPS, backups
Monitoring Dashboards | Uptime Kuma                         | Monitoring, alerting, ops thinking
HTTPS/reverse proxy  | Nginx Proxy Manager                  | Reverse proxy, TLS, hostnames, clean URLs, HTTPS
Secure remote acces  | Cloudflare Tunnel                    | Secure remote access, zero-trust
