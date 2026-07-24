# MITRE ATT&CK Mapping

All detections in this project map to the **Brute Force** technique and its sub-techniques.

| Detection Rule | Tactic | Technique | ID |
| -------------- | ------ | --------- | -- |
| [SSH Failed Password](ssh-failed-password-detection.md) | Credential Access | Brute Force: Password Guessing | [T1110.001](https://attack.mitre.org/techniques/T1110/001/) |
| [Brute-Force Threshold](brute-force-threshold-detection.md) | Credential Access | Brute Force | [T1110](https://attack.mitre.org/techniques/T1110/) |
| [Authentication Failure](authentication-failure-detection.md) | Credential Access | Brute Force | [T1110](https://attack.mitre.org/techniques/T1110/) |
| [Invalid User](invalid-user-detection.md) | Credential Access / Discovery | Brute Force: Password Guessing + Account Discovery | [T1110.001](https://attack.mitre.org/techniques/T1110/001/) · [T1087](https://attack.mitre.org/techniques/T1087/) |

## Notes

- **T1110 — Brute Force:** adversaries systematically guess credentials. All four rules detect symptoms of this behavior in SSH authentication logs.
- **T1110.001 — Password Guessing:** repeated `Failed password` events against known or guessed accounts from a single source IP.
- **T1087 — Account Discovery:** `Invalid user` events reveal an attacker probing for valid usernames before/while guessing passwords.

**Data source:** Linux `sshd` authentication logs (Syslog) → Splunk `index=ssh_bruteforce`.
