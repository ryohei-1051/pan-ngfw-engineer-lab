# pan-ngfw-engineer-lab (GNS3 | HA-first | Linux-only)

## What this repo is
A Palo Alto NGFW Engineer–aligned personal lab built in GNS3.
Focus: HA-first operations + change discipline (runbook/validation/rollback) + evidence-driven troubleshooting.

## Lab goals (mapped to exam domains)
- Networking: zones, interfaces, routing, VPN
- Device operations: HA, logging, certificates/decryption, user mapping
- Integration/automation: PAN-OS API for repeatable changes

## Topology
**Platform:** GNS3 (KVM acceleration assumed)

**Nodes**
- PA-VM-A + PA-VM-B (HA A/P)
- VyOS (ISP + remote site)
- Linux services: web (DMZ), syslog, LDAP/IdM
- Clients: TRUST + REMOTE

**Networks**
- MGMT: 10.10.10.0/24
- TRUST: 10.10.20.0/24
- DMZ: 10.10.30.0/24
- UNTRUST: 192.0.2.0/24
- REMOTE-LAN: 10.10.40.0/24
- VPN-TUN: 10.255.0.0/30

## How to run (GNS3 prerequisites + node sizing)
- Use GNS3 VM (KVM enabled)
- Do not commit vendor images (qcow2/iso) or any license keys

Suggested sizing:
- PA-VM-A: 8GB RAM / 2 vCPU
- PA-VM-B: 8GB RAM / 2 vCPU
- VyOS: 512MB / 1 vCPU
- Linux services: Docker containers preferred

## Modules (HA-first)
- [00 HA foundation + baseline hardening](modules/00-ha-foundation-baseline/)
- [01 Interfaces, zones, routing](modules/01-interfaces-zones-routing/)
- [02 Security policy & NAT](modules/02-security-policy-nat/)
- [03 Logging & monitoring](modules/03-logging-monitoring/)
- [04 VPN: Route-based IPSec to remote site](modules/04-vpn-ipsec-remote-site/)
- [05 Certificates & decryption](modules/05-certificates-decryption/)
- [06 User-ID & group mapping (Linux-only)](modules/06-userid-group-mapping-linux/)
- [07 Automation (PAN-OS API)](modules/07-automation-api/)

## Validation approach
Each module ships with:
- runbook.md (build steps + change control)
- validation.md (tests + expected evidence)
- rollback.md (safe backout)
- evidence/ (screenshots/log samples, sanitized)

## Evidence and sanitization
- No appliance images, licenses, or keys in the repo
- Sanitize screenshots/logs if they include tokens or usernames
- Lab-only RFC1918 addressing

## Known limitations
- Lab ≠ production (performance/features differ)
- Panorama may be added later if resources allow
