# Homelab Architecture

## Infrastructure Diagram

```mermaid
flowchart TD
    Internet[Internet / Minecraft Players]
    DNS[No-IP Dynamic DNS]
    Router[UniFi Dream Router 7]
    Switch[TP-Link Network Switch]

    Internet --> DNS
    DNS -. DNS resolution .-> Router
    Internet -->|Minecraft Traffic| Router
    Router --> Switch

    subgraph Desktop[Windows Desktop]
        VMware[VMware Workstation]

        subgraph Minecraft[minecraft01 - Ubuntu VM]
            MC[Modded Minecraft Server]
            Docker[Docker / Docker Compose]
            Nginx[Nginx]
            Backups[World Backups]
            SSH[SSH Server]

            Docker --> Nginx
            MC --> Backups
        end

        VMware --- Minecraft
    end

    subgraph Monitor[monitor01 - Ubuntu Server]
        Prometheus[Prometheus]
        Grafana[Grafana]
        Ansible[Ansible]
        Python[Python Scripts]

        Grafana --> Prometheus
    end

    Switch --- Desktop
    Switch --- Monitor

    Prometheus -->|Metrics Collection| Minecraft
    Ansible -->|SSH Automation| SSH
```

## Architecture Overview

The homelab consists of two Linux systems with separate
responsibilities for application hosting, infrastructure
monitoring, and automation.

The UniFi Dream Router 7 manages network connectivity,
firewall rules, and external Minecraft access.

The minecraft01 virtual machine hosts the modded
Minecraft server and supporting services.

The monitor01 server hosts infrastructure monitoring
and administrative automation tools.

## Security Considerations

- SSH key-based authentication
- Restricted external service exposure
- Router and firewall management
- Internal monitoring services
- Minecraft world backups

Public IP addresses, credentials, private SSH keys,
and personal connection details are intentionally
excluded from public documentation.
