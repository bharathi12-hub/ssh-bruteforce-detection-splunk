# Authentication Failure Detection

## Rule Name

Authentication Failure Detection

## Description

Detect authentication failures from Linux authentication logs.

## SPL Query

index=ssh_bruteforce "authentication failure"

## Severity

Medium

## Data Source

Linux Syslog Authentication Events

## Investigation

1. Review affected account.
2. Review source host.
3. Determine frequency.
