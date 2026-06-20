# Security Incident Report

## Incident Details

| Field            | Value                      |
| ---------------- | -------------------------- |
| Incident ID      | LAB-SSH-001                |
| Incident Type    | SSH Authentication Failure |
| Severity         | Medium                     |
| Detection Source | Splunk Enterprise          |
| Status           | Closed                     |
| Environment      | Lab                        |

---

## Executive Summary

Multiple SSH authentication failures were detected during security monitoring activities.

Events were collected from a Metasploitable 2 system and forwarded to Splunk Enterprise using Syslog over UDP port 514.

The activity was generated intentionally within a controlled lab environment to validate detection capabilities.

---

## Environment

### Systems Involved

| System            | Role                      |
| ----------------- | ------------------------- |
| Kali Linux        | Event Generation          |
| Metasploitable 2  | Target System             |
| Splunk Enterprise | Log Collection & Analysis |

---

## Timeline

| Stage | Description                       |
| ----- | --------------------------------- |
| T1    | Syslog forwarding configured      |
| T2    | Splunk UDP input configured       |
| T3    | Test message generated            |
| T4    | Authentication failures generated |
| T5    | Events indexed in Splunk          |
| T6    | Detection validated               |

---

## Evidence

### Test Event

```text id="hm1c0n"
SPLUNK_TEST_MESSAGE
```

### Authentication Failure Event

```text id="mjlwmu"
authentication failure
```

### Failed Password Event

```text id="7l7e1x"
Failed password for invalid user fakeuser
```

---

## Investigation

### Searches Performed

```spl id="lktv8f"
index=ssh_bruteforce
```

```spl id="v2c0g1"
index=ssh_bruteforce "Failed password"
```

```spl id="bqq7az"
index=ssh_bruteforce "authentication failure"
```

---

## Findings

* Syslog forwarding functioned correctly.
* Authentication logs were successfully indexed.
* Failed login attempts were detected.
* Security events were searchable through SPL.

---

## Impact Assessment

No actual compromise occurred.

The activity was performed in a controlled cybersecurity lab environment for educational and validation purposes.

---

## Lessons Learned

* Centralized logging improves visibility.
* Splunk simplifies security investigations.
* Authentication logs provide valuable security telemetry.
* Detection content should be documented and validated.

---

## Conclusion

The SSH Brute-Force Detection Lab successfully demonstrated end-to-end log collection, event analysis, and security monitoring using Splunk Enterprise.

Incident Status: Closed
