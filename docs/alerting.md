# Alerting Strategy

## Purpose

Detect suspicious SSH authentication activity and enable rapid investigation.

## Detection Logic

Monitor Syslog events for repeated SSH authentication failures.

## Example Search

```spl
index=ssh_bruteforce "Failed password"
```

## Alert Configuration

| Setting    | Value                         |
| ---------- | ----------------------------- |
| Alert Type | Scheduled                     |
| Schedule   | Every 5 Minutes               |
| Severity   | Medium                        |
| Trigger    | Authentication Failure Events |

## Investigation Workflow

1. Review failed login events.
2. Identify affected accounts.
3. Determine event frequency.
4. Examine source hosts and IP addresses.
5. Escalate suspicious activity if required.

## Benefits

* Faster detection of authentication issues.
* Centralized monitoring through Splunk.
* Improved visibility into system security events.

## Future Improvements

* Correlation searches
* Email notifications
* Dashboard integration
* Automated incident response
