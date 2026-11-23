# Infrastructure Documentation

## Physical Hardware

| Component | Desktop | Monitoring Laptop |
|---|---|---|
| CPU | AMD Ryzen 9 9950X3D | Intel Core i7-8665U |
| RAM | 64 GB DDR5 6000 MHz | 16 GB DDR4 |
| Storage | 6 TB NVMe | 1 TB NVMe |
| GPU | NVIDIA RTX 5090 | Integrated |
| OS | Windows 11 | Ubuntu Server |

## Network Hardware

- UniFi Dream Router 7
- TP-Link 8-port unmanaged switch
- DHCP reservations for persistent IP addresses

## minecraft01

Ubuntu Server virtual machine hosted on VMware Workstation.

Responsibilities:

- Modded Minecraft server hosting
- Docker and Docker Compose
- Nginx web server
- Minecraft world backups
- Infrastructure metrics collection
- SSH remote administration

## monitor01

Dedicated physical Ubuntu Server.

Responsibilities:

- Prometheus metrics collection
- Grafana dashboards
- Ansible configuration management
- Python automation
- Git repository management

## Containerized Services

| Service | Host | Deployment |
|---|---|---|
| Nginx | minecraft01 | Docker Compose |
| Prometheus | monitor01 | Docker Compose |
| Grafana | monitor01 | Docker Compose |

## Design Decisions

- Separate application hosting from infrastructure monitoring.
- Utilize existing hardware to minimize costs.
- Use containers for reproducible service deployments.
- Secure remote administration using SSH keys.
- Maintain infrastructure configurations through Git.
- Automate repetitive administrative tasks using Ansible and Python.
