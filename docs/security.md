# Security Documentation

## Security Overview

The homelab implements security controls to protect internal infrastructure while allowing external players to access the Minecraft server.

## SSH Authentication

Both minecraft01 and monitor01 use SSH key-based authentication for remote administration.

Security practices include:

- ED25519 SSH keys
- Separate keys for GitHub authentication
- Private keys stored securely on authorized systems
- Encrypted remote administration
- SSH access intended for internal network use

## Network Security

The UniFi Dream Router 7 provides network security through:

- Firewall rules
- Network address translation (NAT)
- Controlled port forwarding
- DHCP reservations
- Gateway management

## Service Exposure

| Service | Port | Intended Access |
|---|---|---|
| Minecraft | 25565 | Public |
| SSH | 22 | Internal |
| Grafana | 3000 | Internal |
| Prometheus | 9090 | Localhost |
| Node Exporter | 9100 | Internal |
| Nginx | 80 | Internal |

Only the Minecraft service is intended to be publicly accessible.

## Dynamic DNS

No-IP provides a dynamic DNS hostname for Minecraft players.

Dynamic DNS allows players to connect using a consistent hostname even if the public IP address changes.

## Minecraft Access Control

The Minecraft server currently allows connections without a whitelist.

This simplifies access for invited players but does not prevent uninvited players from connecting.

Enabling a whitelist remains an available security improvement.

## Data Protection

Minecraft world backups are maintained to reduce the risk of data loss caused by corruption, application failures, or administrative errors.

## GitHub Security

Sensitive information is excluded from public repositories, including:

- Private SSH keys
- Passwords
- Authentication tokens
- Public IP addresses
- Personal DDNS hostnames
- Minecraft world save data

## Future Security Improvements

- Enable Minecraft player whitelisting.
- Periodically audit firewall rules.
- Review SSH authentication logs.
- Maintain regular operating system updates.
- Periodically test backup restoration.
- Review container image updates.
