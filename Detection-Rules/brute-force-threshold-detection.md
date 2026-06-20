# Brute Force Threshold Detection

## Rule Name

Multiple Failed Login Attempts

## Description

Identify repeated failed login attempts that may indicate brute-force activity.

## SPL Query

index=ssh_bruteforce "Failed password"
| stats count by host
| where count >= 5

## Severity

High

## MITRE ATT&CK

T1110 - Brute Force

## Investigation

1. Count failures.
2. Identify affected accounts.
3. Review host activity.
4. Escalate if suspicious.
