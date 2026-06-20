# SSH Brute-Force Attack Detection & Monitoring using Splunk

## Overview

This project demonstrates detection and monitoring of SSH brute-force attacks using Splunk SIEM.

A vulnerable Metasploitable machine forwards authentication logs to Splunk via Syslog (UDP 514). Failed login attempts generated during attack simulations are collected, indexed, and analyzed using Splunk searches.

## Objectives

- Simulate SSH brute-force attacks
- Centralize logs using Syslog
- Ingest logs into Splunk
- Detect authentication failures
- Build a foundation for SIEM monitoring and alerting

## Architecture

Kali Linux (Hydra)
        |
        v
Metasploitable
        |
      Syslog
        |
     UDP 514
        |
 Splunk Enterprise
        |
 Searches & Alerts

## Technologies Used

- Splunk Enterprise
- Kali Linux
- Hydra
- Metasploitable 2
- Syslog
- VMware Workstation

## Configuration

### Splunk

- UDP Input: 514
- Source Type: syslog
- Index: ssh_bruteforce

### Metasploitable

Configured `/etc/syslog.conf`:

```bash
*.* @<SPLUNK_IP>
