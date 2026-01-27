# Resources & References

This document contains references used while onboarding multiple log sources into Splunk and troubleshooting ingestion, transport, and normalization challenges in a lab environment.

---

## Splunk Documentation

- **Splunk Enterprise Documentation**  
  https://docs.splunk.com  
  Primary reference for Splunk configuration, inputs, indexing, and searching.

- **UDP and Syslog Data Inputs**  
  https://docs.splunk.com/Documentation/Splunk/latest/Data/Monitornetworkports  
  Used for configuring Splunk to receive syslog data over UDP.

- **Splunk Universal Forwarder Documentation**  
  https://docs.splunk.com/Documentation/Forwarder  
  Reference for installing and managing forwarders on Windows endpoints.

- **Splunk Add-on for Microsoft Windows**  
  https://splunkbase.splunk.com/app/742/  
  Required for proper Windows event log parsing and input configuration.

---

## pfSense & Syslog

- **pfSense System Logging Documentation**  
  https://docs.netgate.com/pfsense/en/latest/monitoring/logs/index.html  
  Reference for configuring local and remote logging in pfSense.

- **RFC 5424 – Syslog Protocol**  
  https://www.rfc-editor.org/rfc/rfc5424  
  Chosen log format for structured messages and precise timestamps.

---

## Linux & Legacy Systems

- **Linux syslog / sysklogd Overview**  
  https://linux.die.net/man/8/sysklogd

- **auth.log Authentication Logging**  
  https://betterstack.com/community/guides/logging/monitoring-linux-auth-logs/

---

## Networking & Port Redirection

- **iptables NAT Table Documentation**  
  https://man7.org/linux/man-pages/man8/iptables.8.html  
  Used to redirect syslog traffic from port 514 to a non-privileged port.

- **iptables-persistent**  
  https://packages.debian.org/iptables-persistent  
  Used to ensure NAT rules persist across system reboots.

---

## Notes

- Official Splunk documentation was treated as the source of truth.
- Legacy system behavior required pragmatic workarounds (syslog + NAT).
- This resource list is intentionally minimal and focused on Project 003.
