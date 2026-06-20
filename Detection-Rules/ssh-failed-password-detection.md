# SSH Failed Password Detection

## Rule Information

| Field        | Value                         |
| ------------ | ----------------------------- |
| Rule Name    | SSH Failed Password Detection |
| Rule Type    | Authentication Monitoring     |
| Severity     | Medium                        |
| Data Source  | Linux Syslog                  |
| Platform     | Splunk Enterprise             |
| MITRE ATT&CK | T1110 - Brute Force           |

---

## Description

This detection identifies failed SSH authentication attempts recorded in Linux authentication logs.

Repeated failed login attempts may indicate:

* Brute-force activity
* Password guessing
* Unauthorized access attempts
* User account enumeration

---

## Detection Logic

The rule searches for SSH authentication events containing the string:

```text id="u9n27x"
Failed password
```

---

## SPL Query

```spl id="55yyx0"
index=ssh_bruteforce "Failed password"
```

---

## Advanced Detection

Detect multiple failed attempts from the same host.

```spl id="g9nq3m"
index=ssh_bruteforce "Failed password"
| stats count by host
| where count >= 5
```

---

## Example Events

```text id="jg4z07"
Failed password for invalid user fakeuser from 192.168.2.128
Failed password for root from 192.168.2.128
```

---

## Investigation Steps

### Step 1

Review affected hosts.

```spl id="5p9j5d"
index=ssh_bruteforce "Failed password"
| stats count by host
```

### Step 2

Review usernames involved.

```spl id="kg89qg"
index=ssh_bruteforce "Failed password"
```

### Step 3

Determine frequency of failures.

### Step 4

Identify suspicious patterns.

### Step 5

Escalate if necessary.

---

## False Positives

* User typing incorrect password
* Service account misconfiguration
* Testing activity within lab environment

---

## Response Actions

* Review authentication logs
* Verify user activity
* Investigate source host
* Reset credentials if necessary

---

## Detection Status

Validated Successfully

Project: SSH Brute-Force Detection & Monitoring using Splunk
