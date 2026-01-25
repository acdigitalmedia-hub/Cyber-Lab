# Resources & References

This document lists references and documentation that were useful for building and validating SSH brute-force detection and alerting in Splunk. These resources helped with understanding log sources, SPL syntax, alert behavior, and how this activity maps to real-world attacker techniques.

---

## Splunk Documentation

- **Splunk Enterprise Documentation (Main Portal)**  
  https://docs.splunk.com  
  Primary reference for Splunk configuration, searching, and alerting.

- **Search & Reporting App Overview**  
  https://docs.splunk.com/Documentation/Splunk/latest/Search/Aboutsearch  
  Overview of how Splunk searches work and how to interpret results.

- **Search Processing Language (SPL) Reference**  
  https://docs.splunk.com/Documentation/Splunk/latest/SearchReference  
  Reference for SPL commands used to build detection logic.

- **Creating Alerts in Splunk**  
  https://docs.splunk.com/Documentation/Splunk/latest/Alert/Aboutalerts  
  Documentation on alert types, trigger conditions, and throttling.

- **inputs.conf Configuration Reference**  
  https://docs.splunk.com/Documentation/Splunk/latest/Admin/Inputsconf  
  Reference for defining data inputs, indexes, and sourcetypes.

---

## Linux & SSH Logging

- **Monitoring Files with Splunk Universal Forwarder**  
  https://docs.splunk.com/Documentation/Splunk/latest/Data/Monitorfilesanddirectories  
  How Splunk ingests file-based logs such as `/var/log/auth.log`.

- **Linux Authentication Logs (auth.log)**  
  PLACEHOLDER – Link to Ubuntu or Debian authentication logging documentation

- **SSH Authentication Logging**  
  PLACEHOLDER – Link to OpenSSH logging and authentication behavior documentation

---

## Offensive Testing & Simulation

- **THC Hydra Documentation**  
  https://github.com/vanhauser-thc/thc-hydra  
  Tool used to simulate SSH brute-force attacks in this lab.

- **Hydra Usage Examples**  
  PLACEHOLDER – Link to Hydra usage or SSH module examples

> Note: Hydra was used strictly in a controlled lab environment for defensive testing and detection validation.

---

## MITRE ATT&CK Framework

- **MITRE ATT&CK – Enterprise Matrix**  
  https://attack.mitre.org  
  Framework used to map observed attacker behavior to standardized techniques.

- **T1110 – Brute Force**  
  https://attack.mitre.org/techniques/T1110/

- **T1110.001 – Password Guessing**  
  https://attack.mitre.org/techniques/T1110/001/

- **T1021.004 – Remote Services: SSH**  
  https://attack.mitre.org/techniques/T1021/004/

---

## Notes

- Official Splunk documentation was treated as the primary source of truth.
- MITRE ATT&CK mappings were used to frame detections in a standardized, threat-informed way.
- This resource list will be expanded as additional detections and alerting logic are added to the lab.
Coming soon
