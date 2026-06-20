# Splunk Searches

## View All Syslog Events

```spl
index=ssh_bruteforce sourcetype=syslog
```

## View Events From Metasploitable

```spl
host=METASPLOITABLE
```

## Search Failed Password Events

```spl
index=ssh_bruteforce "Failed password"
```

## Search Authentication Failures

```spl
index=ssh_bruteforce "authentication failure"
```

## Verify Test Message Ingestion

```spl
index=ssh_bruteforce SPLUNK_TEST_MESSAGE
```

## View Recent Events

```spl
index=ssh_bruteforce
| sort - _time
```

## Event Statistics

```spl
index=ssh_bruteforce
| stats count by host
```

## Security Use Cases

* Verify Syslog ingestion.
* Monitor authentication failures.
* Investigate suspicious login activity.
* Validate SIEM data collection.
