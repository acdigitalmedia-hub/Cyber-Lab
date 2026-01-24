# Splunk Enterprise – Installation & Basic Configuration

## Overview

Splunk is one of those tools that shows up *constantly* in cybersecurity job postings, especially for SOC, detection, and incident response roles. While I’ve previously worked with Wazuh in my lab, I wanted to spend time understanding Splunk from the ground up: how it’s installed, how data gets into it, and what “working” actually looks like once logs are flowing.

This project focuses on getting a functional Splunk Enterprise deployment running in my lab, ingesting logs from both Windows and Linux systems, and validating that data is searchable. The goal wasn’t to build anything fancy yet, just to establish a solid foundation I can expand on later.

---

## Lab Environment

My lab runs on a Proxmox VE server and already includes several core components:

- Windows Server 2025 (Domain Controller)
- Kali Linux VM
- Ubuntu Server (Docker host)
- Internal lab network (`vmbr2`)

Splunk Enterprise is deployed as an LXC container within Proxmox.

> **Note:** I used the Proxmox VE Helper Script to deploy Splunk Enterprise. I’m aware some people prefer not to run scripts directly on the Proxmox host. For this test lab, I’m comfortable with that tradeoff, but I’ve included a manual installation alternative below.

📸 **Screenshot:** Proxmox VM/LXC overview showing existing lab components
![Proxmox VM/LXC overview showing existing lab components](/Screenshots/existing proxmox.png)

---

## Deploying Splunk Enterprise (Proxmox LXC)

https://community-scripts.github.io/ProxmoxVE/scripts?id=splunk-enterprise

Using the Proxmox VE helper script, I deployed a Splunk Enterprise LXC container with mostly default settings. The only change I made was adjusting the network bridge:

- **Network bridge:** `vmbr2` (my internal lab network)
- **VLAN tag:** none

Once the container finished provisioning, the script generated a `splunk.creds` file containing the initial login credentials.

📸 **Screenshot:** Proxmox console showing Splunk container creation  
📸 **Screenshot:** `splunk.creds` file (credentials redacted)

---

## Alternative: Manual Installation (Optional Path)

If you prefer not to use helper scripts, Splunk Enterprise can also be installed manually by following Splunk’s official documentation and installing it directly on an existing Linux server. The rest of the configuration steps in this project remain the same regardless of deployment method.

---

## First Login (Sanity Check)

From my Kali Linux VM, I navigated to the Splunk Web interface using the IP address and port specified during installation.

After logging in with the credentials from `splunk.creds` success! Splunk was up and running.

📸 **Screenshot:** Splunk login page  
📸 **Screenshot:** Splunk dashboard after first login

Now the real question: **what do I actually do with it?**

---

## Configuring Splunk to Receive Data

The first step was enabling Splunk to receive data from forwarders.

1. In Splunk Web, I navigated to:
   **Settings → Forwarding and Receiving**
2. Under **Receive data**, I clicked **Add new**
3. Set the listening port to **9997**

📸 **Screenshot:** Forwarding and Receiving settings  
📸 **Screenshot:** Port 9997 configured for receiving data

---

## Installing the Splunk Universal Forwarder (Windows)

To start ingesting logs, I installed the Splunk Universal Forwarder on my Windows Server 2025 domain controller.

Steps:
1. Navigated to the Splunk website
2. Created/logged into an account
3. Downloaded the Windows Universal Forwarder installer
4. Installed it on the domain controller

During setup, I configured:
- **Deployment server:** `<Splunk-IP>:8089`
- **Receiving indexer:** `<Splunk-IP>:9997`

📸 **Screenshot:** Universal Forwarder setup wizard (server configuration)

---

## Ingesting Windows Event Logs

Initially, I attempted to configure ingestion through the Splunk GUI:

- **Settings → Add Data → Forward**
- Selected the domain controller as a data source
- Configured it to send all local event logs
- Created a new index named `windows`

However, I ran into some friction and decided to configure it manually instead.

### Manual Configuration (Windows)

On the Windows Server 2025 system:

1. Opened **Notepad as Administrator**
2. Edited: C:\Program Files\SplunkUniversalForwarder\etc\system\local\inputs.conf
3. Added the following:

```ini
[WinEventLog://Application]
disabled = 0
index = windows

[WinEventLog://Security]
disabled = 0
index = windows

[WinEventLog://System]
disabled = 0
index = windows
```

4. Saved the file
    
5. Restarted the **SplunkForwarder** service via `services.msc`
    

> **IMPORTANT:** The `windows` index must already exist in Splunk (**Settings → Indexes**) or the data will be dropped. If it doesn't exist, that's okay it's very easy to add. Just go to **Settings → Indexes** and click "New Index". Type in "windows" as the name and click save. Piece of cake!

📸 **Screenshot:** inputs.conf configuration  
📸 **Screenshot:** Windows Services showing SplunkForwarder restart

### Validation

In Splunk:

- Navigated to **Apps → Search & Reporting**
    
- Ran the following query:
    

`index=windows`

Logs appeared which means indexing was working!

📸 **Screenshot:** Windows event logs in Splunk search

---

## Installing the Universal Forwarder (Ubuntu)

Next, I repeated the process on my Ubuntu server.

### Installation

1. Downloaded the forwarder using `wget`
    
2. Installed it:
    

`sudo dpkg -i splunkforwarder-<version>.deb`

3. Started Splunk and accepted the license:
    

`sudo /opt/splunkforwarder/bin/splunk start --accept-license`

4. Configured the forwarding destination:
    

`sudo /opt/splunkforwarder/bin/splunk add forward-server <Splunk-IP>:9997`

📸 **Screenshot:** Ubuntu terminal showing forwarder install and startup

---

## Ingesting Linux Logs

On the Ubuntu server:

1. Edited:
    

`/opt/splunkforwarder/etc/system/local/inputs.conf`

2. Added a stanza to monitor authentication logs:
    

```
[monitor:///var/log/auth.log]
disabled = 0
index = linux_logs
```

3. Restarted the forwarder:
    

`sudo /opt/splunkforwarder/bin/splunk restart`

📸 **Screenshot:** Linux inputs.conf configuration

### Validation

In Splunk:

`index=linux_logs`

Linux logs appeared successfully.

📸 **Screenshot:** Linux logs in Splunk search

---

## Result

At this point, Splunk was successfully ingesting logs from:

- Windows Server 2025 (event logs)
    
- Ubuntu Server (auth logs)
    

This gave me a working Splunk environment with real data flowing in which is a solid baseline to build on.

---

## What I Learned

- Splunk is straightforward to stand up, but understanding _how data actually flows_ is key
    
- Index creation matters more than I initially expected
    
- Manual configuration is sometimes clearer than the GUI
    
- Validation searches are essential! Just because it says “installed” doesn’t mean it's “working”
    

---

## Next Steps

Some ideas I plan to explore next:

- Normalizing Windows and Linux data with Splunk apps
    
- Writing basic detection searches
    
- Dashboards for authentication activity
    
- Exploring alerts and correlation
    
- Comparing Splunk workflows to Wazuh
