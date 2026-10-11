# Home Lab

A home server and security lab built on old hardware and a small budget, written up one phase at a time.

I'm Grace. I work in IT and I'm moving into cybersecurity, with a focus on vulnerability management, Microsoft Sentinel, Azure, and Tenable.

This lab is how I'm learning it for real. I build each piece myself in my apartment, break it, fix it, and then write down what happened. Every phase has a write-up with what I built, why I made each choice, the steps, and what went wrong. The mistakes stay in on purpose. They're where I learned the most.

I ask "why" at every step, so you'll find the reasons next to the commands. If you're starting out and wondering whether you need expensive gear or years of experience first, you don't. I started with a desktop I already had and a lot of questions.

## Goals

1. Run a hypervisor on a single small form factor PC.
2. Build NAS storage with a tested backup.
3. Segment the network so the lab is isolated from the home network.
4. Self-host a movie server for home use.
5. Run a security lab for vulnerability scanning and log analysis.
6. Run small AI models locally.
7. Document everything here.

## Hardware

| Device | Specs | Role |
|---|---|---|
| HP EliteDesk 800 G3 SFF | Intel Core i5-7500 (4 cores), 16GB DDR4, 256GB NVMe | Main server, Proxmox VE host |
| Lenovo ThinkPad X1 Carbon Gen 8 | Intel Core i7 (10th gen), 16GB RAM | Local AI box (planned) |
| Raspberry Pi 3B+ | 1GB RAM | DNS filtering or monitoring (planned) |
| Two unmanaged 5 port gigabit switches | TP-Link TL-SG105, Netgear GS105 | Extra ports inside a single VLAN |
| External USB drives | 5TB and 2TB | Data migration source, then NAS backup target |

Parts budget for the whole project: 200 to 300 USD. Everything else is hardware I already had.

## Architecture

| Layer | Choice | Why |
|---|---|---|
| Hypervisor | Proxmox VE | Runs the firewall, NAS, containers, and lab targets on one box. Free and well documented |
| Containers | One Debian VM dedicated to Docker, services defined with Docker Compose | Containers use less RAM than full VMs, and the Compose files live in this repo |
| Firewall | OPNsense as a VM, VLAN trunk on a single NIC (planned) | Isolates the lab without replacing the home router |
| Storage | One internal NAS drive with a scheduled backup to an external drive (planned) | The chassis has one 3.5" bay, and a backup protects against more failures than a mirror |
| Home network | ISP router stays in place, lab sits behind it | Home internet does not depend on the lab |

## Roadmap

| Phase | What | Status |
|---|---|---|
| 1 | Foundation: Proxmox VE, Docker VM, this repo | Done. [Write-up](docs/phase-1-foundation.md) |
| 2 | NAS storage, data migration, tested backup | Not started |
| 3 | Network segmentation: OPNsense, VLANs, managed switch | Not started |
| 4 | Movie server in Docker with hardware transcoding | Not started |
| 5 | Security lab: vulnerability scanning with Tenable, vulnerable targets, log forwarding to Microsoft Sentinel | Not started |
| 6 | Local AI with Ollama | Not started |

## Repository layout

```
docs/       Phase write-ups
docker/     Docker Compose files, one folder per service
diagrams/   Network and architecture diagrams
```

## A note on what is not here

Configs and screenshots are sanitized before they are committed. This repo contains no passwords, keys, public IP addresses, or serial numbers, and nothing from any employer.

## More of my work

My other security projects are in my [cybersecurity portfolio](https://github.com/GMACperspectives/cybersecurity-portfolio).
