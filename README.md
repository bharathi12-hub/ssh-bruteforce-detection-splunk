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
## Screenshots

### 1. Syslog Events Ingested
![Syslog Events](screenshots/01-syslog-events-ingested.png)

### 2. Additional Syslog Events
![Syslog Events Alt](screenshots/02-syslog-events-ingested-alt.png)

### 3. Metasploitable Host Search
![Host Search](screenshots/03-host-metasploitable-search.png)

### 4. Host Search Results
![Host Results](screenshots/04-host-search-results.png)

### 5. Splunk Test Message Verification
![Test Message](screenshots/05-splunk-test-message.png)

### 6. SSH Brute-Force Events
![SSH Brute Force](screenshots/06-ssh-bruteforce-events.png)

### 7. SSH Brute-Force Index Search
![Index Search](screenshots/07-ssh-bruteforce-index-search.png)
