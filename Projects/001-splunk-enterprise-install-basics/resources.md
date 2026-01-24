# Resources & References

This document contains documentation, guides, and reference material I found useful while installing and configuring Splunk Enterprise and the Splunk Universal Forwarder. These resources were used both to validate my approach and to better understand how Splunk is designed to operate in real environments.

---

## Official Splunk Documentation

- **Splunk Enterprise Documentation (Main Portal)**  
  https://docs.splunk.com  
  Authoritative reference for installation, configuration, and administration.

- **Splunk Enterprise Installation Guide**  
  https://docs.splunk.com/Documentation/Splunk/latest/Installation  
  Step-by-step guidance for installing Splunk Enterprise across supported platforms.

- **Splunk Web (Admin Interface) Overview**  
  https://docs.splunk.com/Documentation/Splunk/latest/Admin  
  Reference for administrative settings, indexes, forwarding, and receiving.

---

## Splunk Forwarder Resources

- **Splunk Universal Forwarder Documentation**  
  https://docs.splunk.com/Documentation/Forwarder  
  Official documentation covering forwarder installation and configuration.

- **Universal Forwarder Installation – Windows**  
  https://docs.splunk.com/Documentation/Forwarder/latest/Forwarder/Installtheuniversalforwarder  
  Platform-specific installation details for Windows systems.

- **Universal Forwarder Installation – Linux**  
  https://docs.splunk.com/Documentation/Forwarder/latest/Forwarder/Installtheuniversalforwarder  
  Platform-specific installation details for Linux systems.

---

## Configuration References

- **inputs.conf Configuration Reference**  
  https://docs.splunk.com/Documentation/Splunk/latest/Admin/Inputsconf  
  Detailed explanation of inputs.conf stanzas and options.

- **Receiving Data (ports, forwarding, indexes)**  
  https://docs.splunk.com/Documentation/Splunk/latest/Forwarding/Receivingdata  
  Explanation of how Splunk receives data from forwarders.

- **Indexes and Index Management**  
  https://docs.splunk.com/Documentation/Splunk/latest/Admin/Indexes  
  How indexes work, how to create them, and common pitfalls.

---

## Windows Event Log Ingestion

- **Monitor Windows Event Logs**  
  https://docs.splunk.com/Documentation/Splunk/latest/Data/MonitorWindowseventlogdata  
  How Splunk ingests Windows Event Logs via the Universal Forwarder.

- **Windows Event Log Channel Reference**  
  https://learn.microsoft.com/en-us/windows/win32/eventlog/event-log-channels  
  Microsoft reference for understanding Windows event log channels and structure.

---

## Linux Log Ingestion

- **Monitor Files and Directories**  
  https://docs.splunk.com/Documentation/Splunk/latest/Data/Monitorfilesanddirectories  
  Reference for monitoring Linux log files using the Universal Forwarder.


---

## Proxmox & Lab Environment

- **Proxmox VE Documentation**  
  https://pve.proxmox.com/pve-docs/  
  Official documentation for Proxmox VE configuration and management.

- **Proxmox VE Helper Scripts**  
  https://community-scripts.github.io/ProxmoxVE/  
  (Used in this lab to deploy Splunk Enterprise as an LXC container)

> **Note:** Helper scripts are convenient but should be evaluated carefully before use in production environments.

---

## Search & SPL Fundamentals

- **Search & Reporting App Overview**  
  https://docs.splunk.com/Documentation/Splunk/latest/Search/Aboutsearch  
  Introduction to searching and reporting in Splunk.

- **Search Processing Language (SPL) Reference**  
  https://docs.splunk.com/Documentation/Splunk/latest/SearchReference  
  Comprehensive reference for SPL commands and syntax.

---

## Learning & Community Resources

- **Splunk Fundamentals (Free Training)**  
  https://www.splunk.com/en_us/training/free-courses/splunk-fundamentals-1.html  
  Entry-level course covering Splunk basics and workflows.

- **Splunk Community (Answers & Discussions)**  
  https://community.splunk.com  
  Community Q&A, examples, and troubleshooting discussions.

---

## Notes

- Official documentation was the primary source of truth for configuration details.
- Community discussions were useful for understanding common pitfalls and real-world deployment considerations.
- This resource list may continue to grow as I explore more advanced Splunk features and use cases.
