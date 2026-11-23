# Homelab Operations Runbook

## Purpose

This runbook provides operational procedures for maintaining, troubleshooting, and recovering the Minecraft homelab infrastructure.

## Infrastructure Startup

1. Verify that the UniFi gateway and network switch are operational.
2. Power on the primary Windows desktop.
3. Start or resume minecraft01 in VMware Workstation.
4. Verify that the Minecraft server is running.
5. Verify that monitor01 is online.
6. Verify that monitoring containers are running.
7. Confirm that Grafana is receiving metrics.
8. Test Minecraft connectivity.

## Linux Health Checks

Check system uptime and load:

```bash
uptime
```

Check memory utilization:

```bash
free -h
```

Check disk utilization:

```bash
df -h
```

Check IP addressing:

```bash
ip -4 -br addr
```

Check failed system services:

```bash
systemctl --failed
```

Check SSH service:

```bash
sudo systemctl status ssh
```

## Docker Operations

List running containers:

```bash
sudo docker ps
```

List all containers:

```bash
sudo docker ps -a
```

Check container resource utilization:

```bash
sudo docker stats --no-stream
```

## Monitoring Operations

Execute on monitor01:

```bash
cd ~/monitoring
sudo docker compose ps
```

Start monitoring services:

```bash
sudo docker compose up -d
```

Review monitoring logs:

```bash
sudo docker compose logs --tail=50
```

Restart monitoring services:

```bash
sudo docker compose restart
```

## Minecraft Server Troubleshooting

If players cannot connect:

1. Verify minecraft01 is running.
2. Verify the Minecraft server is running.
3. Check whether port 25565 is listening.
4. Verify local network connectivity.
5. Verify UniFi port forwarding and firewall rules.
6. Verify dynamic DNS resolution.
7. Verify client and server modpack versions match.
8. Review Minecraft server logs.

Check the listening port:

```bash
sudo ss -lntp | grep 25565
```

## Backup and Recovery

- Verify that scheduled backups are being generated.
- Review backup timestamps and available disk space.
- Stop the Minecraft server gracefully before restoring world data.
- Preserve the existing world before attempting restoration.
- Restore from a known-good backup.
- Verify world integrity after restarting the server.

Reference:

[Minecraft Homelab Backups](https://github.com/Aaron24000/minecraft-homelab-backups)

## Linux Maintenance

Check available updates:

```bash
sudo apt update
apt list --upgradable
```

Apply updates during a planned maintenance window:

```bash
sudo apt upgrade
```

Review recent system errors:

```bash
sudo journalctl -p err -n 50
```

## Graceful Shutdown

1. Notify connected Minecraft players.
2. Save the Minecraft world.
3. Stop the Minecraft server gracefully.
4. Verify backup completion.
5. Shut down minecraft01.
6. Shut down monitor01 if required.

Linux shutdown command:

```bash
sudo shutdown -h now
```

## Recommended Maintenance Schedule

| Frequency | Task |
|---|---|
| Daily | Verify server availability and backups |
| Weekly | Review Grafana dashboards |
| Weekly | Review disk and memory utilization |
| Monthly | Review operating system updates |
| Monthly | Review firewall configuration |
| Monthly | Test backup restoration |
| As needed | Update infrastructure documentation |

## Known Issues

- Automatic virtual machine startup and resume behavior requires further investigation.
- External Minecraft connectivity should be validated with remote players.

## Change Management

Infrastructure changes should be tested, documented, and committed to the appropriate Git repository.

Credentials, private keys, and sensitive network information must not be committed to public repositories.
