# Invalid User Detection

## Rule Name

Invalid User Authentication Attempt

## Description

Detect login attempts using usernames that do not exist on the target system.

## SPL Query

index=ssh_bruteforce "Invalid user"

## Severity

Medium

## MITRE ATT&CK

T1110 - Brute Force

## Investigation

1. Review username.
2. Review event frequency.
3. Determine whether activity is expected.
