# Sample Data

`auth.log` is a small, sanitized set of Linux `sshd` authentication events that reproduce the
detections in this project **without needing the full VM lab**. It includes failed passwords,
invalid users, a PAM authentication-failure line, and one successful login, from two source IPs.

## Load it into Splunk

One-shot index into the project index:

```bash
splunk add oneshot ./auth.log -index ssh_bruteforce -sourcetype syslog
```

…or upload via **Settings → Add Data → Upload**, setting sourcetype `syslog` and index
`ssh_bruteforce`.

## Try a detection

```spl
index=ssh_bruteforce "Failed password" | stats count by src_ip | where count >= 5
```

`192.168.2.128` should cross the threshold, matching the alert in
[`../splunk-config/savedsearches.conf`](../splunk-config/savedsearches.conf).
