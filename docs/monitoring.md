# Infrastructure Monitoring

## Overview

The homelab uses Prometheus and Grafana to provide centralized infrastructure monitoring. Both services are deployed as Docker containers on monitor01 using Docker Compose.

## Monitoring Stack

| Component | Purpose |
|---|---|
| Prometheus | Metrics collection and time-series storage |
| Grafana | Dashboard visualization |
| Node Exporter | Linux system metrics |
| Docker Compose | Monitoring stack deployment |

## Metrics Collection

Prometheus collects infrastructure metrics from configured monitoring targets.

Monitored system resources include:

- CPU utilization
- Memory utilization
- Disk space utilization
- Network activity
- System uptime
- Host availability

## Grafana

Grafana uses Prometheus as a data source to visualize infrastructure metrics.

Dashboards provide visibility into system health, resource consumption, and potential performance issues.

## Service Management

The monitoring stack is maintained in the ~/monitoring directory on monitor01.

Check container status:

```bash
cd ~/monitoring
sudo docker compose ps
```

Start monitoring services:

```bash
sudo docker compose up -d
```

View service logs:

```bash
sudo docker compose logs --tail=50
```

Restart monitoring services:

```bash
sudo docker compose restart
```

## Network Access

| Service | Port | Access |
|---|---|---|
| Grafana | 3000 | Internal network |
| Prometheus | 9090 | Localhost on monitor01 |

Monitoring services are not intentionally exposed to the public internet.

## Troubleshooting

If monitoring data becomes unavailable:

1. Verify that the monitoring containers are running.
2. Check Prometheus target availability.
3. Verify Node Exporter availability.
4. Check network connectivity between hosts.
5. Verify the Grafana data source configuration.
6. Review container logs.

## Design Decisions

- Separate monitoring from application hosting.
- Centralize infrastructure metrics collection.
- Use Docker Compose for reproducible deployment.
- Restrict external access to monitoring services.
- Use dashboards to identify resource bottlenecks and infrastructure issues.

## Prometheus Monitoring Targets

| Target | Purpose | Scrape Interval |
|---|---|---|
| cAdvisor | Docker container resource metrics | 15 seconds |
| minecraft01 | Minecraft VM system metrics | 15 seconds |
| monitor01 | Monitoring host system metrics | 15 seconds |
| Prometheus | Prometheus self-monitoring | 15 seconds |

All four targets were verified as healthy during infrastructure validation on November 23, 2026.

## cAdvisor

cAdvisor provides container-level monitoring on minecraft01, including:

- Container CPU utilization
- Container memory utilization
- Container network activity
- Container filesystem metrics

Prometheus collects these metrics for visualization through Grafana.

## Secure Prometheus Access

Prometheus is bound to localhost on monitor01.

Its web interface can be accessed remotely using SSH local port forwarding without exposing port 9090 to the network.
