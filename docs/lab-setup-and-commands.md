# Complete Lab Setup and Commands

## Project Overview

This document contains all commands, configurations, validation steps, and troubleshooting procedures used to build the SSH Brute-Force Detection & Monitoring Lab using Splunk Enterprise.

---

# Lab Architecture

```text
Windows 11 Host
│
├── Splunk Enterprise
│
├── Kali Linux VM
│   └── Attack Simulation
│
└── Metasploitable 2 VM
    └── Vulnerable SSH Service
```

---

# Network Configuration

## Windows 11 Host

### Display Network Information

```powershell id="c9u0x4"
ipconfig
```

### Verify VMware NAT Adapter

```powershell id="cv7n6v"
ipconfig /all
```

### Test Connectivity

```powershell id="h7ay30"
ping 192.168.21.136
```

### Verify UDP Port 514

```powershell id="p56sfi"
netstat -ano -p udp | findstr 514
```

### Configure Firewall Rule

```powershell id="k8p7d0"
New-NetFirewallRule `
-DisplayName "Splunk Syslog UDP 514" `
-Direction Inbound `
-Protocol UDP `
-LocalPort 514 `
-Action Allow
```

---

# Splunk Enterprise Setup

## Access Splunk

```text id="4u5h1x"
http://localhost:8000
```

## Create Index

Settings → Indexes → New Index

```text id="jlwmh5"
Index Name:
ssh_bruteforce
```

## Create UDP Input

Settings → Data Inputs → UDP → New Local UDP

```text id="9e6lhl"
Port: 514
Source Type: syslog
Index: ssh_bruteforce
```

## Verify Input

Settings → Data Inputs → UDP

Expected:

```text id="lcrtxv"
Port: 514
Status: Enabled
Index: ssh_bruteforce
```

---

# Kali Linux Commands

## View Network Interface

```bash id="9lg29s"
ip a
```

## View Routing Table

```bash id="qwl7ea"
ip route
```

## Test Target Connectivity

```bash id="yjlwmx"
ping 192.168.21.136
```

## Verify SSH Service

```bash id="1pn0yj"
nmap -sV 192.168.21.136
```

## Verify Port 22

```bash id="h08x0f"
nmap -p 22 192.168.21.136
```

## Verify Host Discovery

```bash id="y8x20i"
nmap -sn 192.168.21.0/24
```

---

# Metasploitable 2 Commands

## Display IP Address

```bash id="jrm37n"
ifconfig
```

## Display Routing Table

```bash id="yq0d2q"
route -n
```

## Display ARP Table

```bash id="2b0i0p"
arp -a
```

## Verify Kali Connectivity

```bash id="l8l4vb"
ping -c 4 192.168.21.129
```

## Edit Syslog Configuration

```bash id="q7u0j4"
nano /etc/syslog.conf
```

Add:

```text id="p71z4h"
*.* @192.168.21.19
```

## Verify Configuration

```bash id="1lmgdn"
grep "@192.168.21.19" /etc/syslog.conf
```

Expected:

```text id="z7f2ki"
*.* @192.168.21.19
```

## Restart Syslog Service

```bash id="ftngd0"
/etc/init.d/sysklogd restart
```

Expected:

```text id="ewbtmy"
* Restarting system log daemon... [ OK ]
```

---

# Log Generation

## Generate Test Event

```bash id="vg5s0f"
logger "SPLUNK_TEST_MESSAGE"
```

Purpose:

```text id="kwjclq"
Verify Syslog forwarding to Splunk.
```

## Generate Authentication Failure Events

```bash id="d86y0o"
ssh fakeuser@localhost
```

Enter incorrect passwords multiple times.

Expected Events:

```text id="df7y4g"
Failed password
Invalid user
authentication failure
```

---

# Splunk Investigation Queries

## View All Events

```spl id="0whj6g"
index=ssh_bruteforce
```

## View Syslog Events

```spl id="3l80m2"
index=ssh_bruteforce sourcetype=syslog
```

## Search Test Event

```spl id="k5zc0w"
index=ssh_bruteforce SPLUNK_TEST_MESSAGE
```

## Search Authentication Failures

```spl id="pnl14i"
index=ssh_bruteforce "authentication failure"
```

## Search Failed Password Events

```spl id="e2cg2n"
index=ssh_bruteforce "Failed password"
```

## Search Invalid Users

```spl id="ympvca"
index=ssh_bruteforce "Invalid user"
```

## Search Metasploitable Events

```spl id="jlwm6j"
host=METASPLOITABLE
```

---

# Troubleshooting

## No Events Appearing

Verify UDP Listener:

```powershell id="32iw3q"
netstat -ano -p udp | findstr 514
```

Verify Syslog Configuration:

```bash id="h1r65n"
grep "@192.168.21.19" /etc/syslog.conf
```

Verify Service Status:

```bash id="cdy6g6"
/etc/init.d/sysklogd restart
```

Verify Network Connectivity:

```bash id="ltj3d7"
ping 192.168.21.19
```

---

# Validation Checklist

## Infrastructure

* [x] Windows Host Operational
* [x] Splunk Enterprise Installed
* [x] Kali Linux Connected
* [x] Metasploitable Connected

## Log Collection

* [x] UDP 514 Input Configured
* [x] Syslog Forwarding Enabled
* [x] Test Message Received

## Detection

* [x] Authentication Failures Detected
* [x] Failed Password Events Detected
* [x] Invalid User Events Detected

## Investigation

* [x] SPL Queries Verified
* [x] Event Search Functional
* [x] End-to-End Pipeline Operational

```
```
