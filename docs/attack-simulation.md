# Attack Simulation

## Objective

The objective of this simulation is to generate SSH authentication failures and verify that security events are successfully collected and analyzed in Splunk.

## Lab Environment

| Component         | Purpose                     |
| ----------------- | --------------------------- |
| Kali Linux        | Attack Machine              |
| Hydra             | Brute-Force Tool            |
| Metasploitable 2  | Vulnerable Target           |
| Syslog            | Log Forwarding              |
| Splunk Enterprise | Log Collection and Analysis |

## Methodology

1. Configure Metasploitable to forward logs to Splunk using Syslog.
2. Verify successful log ingestion in Splunk.
3. Simulate SSH authentication failures against the target system.
4. Search and analyze generated events within Splunk.
5. Validate detection of failed login attempts.

## Expected Outcome

* Authentication failures are generated.
* Syslog forwards events to Splunk.
* Events are indexed successfully.
* Security analysts can identify suspicious SSH activity through Splunk searches.

## Conclusion

The simulation demonstrates how Splunk can be used to collect, index, and investigate SSH authentication failures in a controlled lab environment.
