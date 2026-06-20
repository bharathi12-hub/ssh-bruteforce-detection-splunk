# SSH Brute-Force Attack Detection & Monitoring using Splunk

## Overview

This project demonstrates the detection and monitoring of SSH brute-force attacks using Splunk SIEM.

A vulnerable Metasploitable 2 machine forwards authentication logs to Splunk Enterprise through Syslog (UDP 514). Authentication failures generated during testing are collected, indexed, and analyzed using Splunk Search Processing Language (SPL).

The project showcases how security analysts can centralize logs, investigate failed login attempts, and build foundational SIEM detection workflows.

---

## Objectives

* Simulate SSH authentication failures in a controlled lab environment
* Configure Syslog-based log forwarding
* Ingest Linux authentication logs into Splunk
* Analyze authentication-related security events
* Build basic SIEM monitoring capabilities
* Demonstrate security event investigation using SPL queries

---

## Architecture

```text
Kali Linux (Attacker)
        |
        | SSH Login Attempts
        v
Metasploitable 2 (Target)
        |
        | Syslog Events
        v
UDP 514
        |
        v
Splunk Enterprise
        |
        v
Searches, Monitoring & Analysis
```

---

## Technologies Used

| Technology         | Purpose                      |
| ------------------ | ---------------------------- |
| Splunk Enterprise  | Log collection and analysis  |
| Kali Linux         | Attack simulation            |
| Metasploitable 2   | Vulnerable target system     |
| Syslog             | Log forwarding               |
| VMware Workstation | Virtualization platform      |
| Linux              | System administration        |
| SPL                | Security event investigation |

---

## Lab Environment

| Machine           | Role          |
| ----------------- | ------------- |
| Kali Linux        | Attacker      |
| Metasploitable 2  | Target        |
| Splunk Enterprise | SIEM Platform |

---

## Configuration

### Splunk Configuration

* UDP Input Port: 514
* Source Type: syslog
* Index: ssh_bruteforce

### Metasploitable Configuration

Edit:

```bash
/etc/syslog.conf
```

Configure Syslog forwarding:

```bash
*.* @<SPLUNK_IP>
```

Restart Syslog service after configuration changes.

---

## Event Verification

Verify log ingestion using test messages and authentication-related events.

Example SPL Queries:

### View All Syslog Events

```spl
index=ssh_bruteforce sourcetype=syslog
```

### View Events From Metasploitable

```spl
host=METASPLOITABLE
```

### Search Authentication Failures

```spl
index=ssh_bruteforce "authentication failure"
```

### Search Failed Password Events

```spl
index=ssh_bruteforce "Failed password"
```

---

## Project Workflow

1. Configure Syslog forwarding on Metasploitable.
2. Configure Splunk UDP input.
3. Verify log ingestion using test messages.
4. Generate authentication-related events.
5. Search and analyze events in Splunk.
6. Investigate authentication failures using SPL queries.

---

## Documentation

Additional project documentation is available in the `/docs` folder:

* architecture.md
* attack-simulation.md
* splunk-searches.md
* alerting.md

---

## Screenshots

### 1. Syslog Events Successfully Ingested

![Syslog Events](screenshots/01-syslog-events-ingested.png)

### 2. Additional Syslog Events

![Syslog Events Alt](screenshots/02-syslog-events-ingested-alt.png)

### 3. Metasploitable Host Search

![Host Search](screenshots/03-host-metasploitable-search.png)

### 4. Host Search Results

![Host Results](screenshots/04-host-search-results.png)

### 5. Splunk Test Message Verification

![Test Message](screenshots/05-splunk-test-message.png)

### 6. Authentication Failure Events

![Authentication Events](screenshots/06-ssh-bruteforce-events.png)

### 7. SSH Brute-Force Event Investigation

![Index Search](screenshots/07-ssh-bruteforce-index-search.png)

---

## Skills Demonstrated

* Security Information and Event Management (SIEM)
* Log Collection and Management
* Splunk Enterprise Administration
* Security Event Analysis
* Linux Log Monitoring
* Syslog Configuration
* Search Processing Language (SPL)
* Incident Investigation
* Security Operations (SOC) Fundamentals

---

## Future Enhancements

* Real-time alerting
* Custom Splunk dashboards
* Correlation searches
* Threat intelligence enrichment
* Automated incident response workflows
* Detection rule tuning

---

## Author

**Bharathithasan S**

Cyber Security Student | Splunk | SIEM | Linux | Security Monitoring
