# Splunk Configuration

Reusable Splunk configuration for this SSH brute-force detection lab. Copy these files into a
dedicated app (recommended) at `$SPLUNK_HOME/etc/apps/ssh_bruteforce/local/`, or into
`$SPLUNK_HOME/etc/system/local/`, then restart Splunk.

| File | Purpose |
| ---- | ------- |
| `inputs.conf` | UDP 514 Syslog input → `index=ssh_bruteforce` |
| `props.conf` | Search-time field extractions (`user`, `src_ip`, `src_port`) for sshd events |
| `savedsearches.conf` | Scheduled brute-force alert (5+ failures / 15 min / source IP) |

**Before you start:**

1. Create the `ssh_bruteforce` index: **Settings → Indexes → New Index**.
2. Open UDP 514 on the Splunk host's firewall.
3. Restart Splunk after copying the `.conf` files.

You can validate the extractions and alert against the sample data in
[`../sample-data/`](../sample-data/) without building the full VM lab.
