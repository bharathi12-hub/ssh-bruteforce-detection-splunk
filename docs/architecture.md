# Architecture

## Overview

This project demonstrates SSH brute-force attack detection using Splunk SIEM.

## Components

- Kali Linux (Attacker)
- Metasploitable 2 (Target)
- Syslog (UDP 514)
- Splunk Enterprise

## Data Flow

Kali Linux (Hydra)
      |
      v
Metasploitable SSH Service
      |
      v
Syslog Forwarding (UDP 514)
      |
      v
Splunk Enterprise
      |
      v
Searches, Dashboards, and Alerts
