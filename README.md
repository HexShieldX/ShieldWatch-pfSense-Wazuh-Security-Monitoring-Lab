## ShieldWatch: pfSense & Wazuh Security Monitoring Lab

## Overview

SentinelWall is an enterprise-style cybersecurity lab focused on integrating pfSense Community Edition with Wazuh to simulate real-world Security Operations Center (SOC) monitoring and threat detection workflows.

The project demonstrates centralized log collection, firewall monitoring, custom log parsing, GeoIP-based traffic filtering, DNS-based content blocking, and security event analysis within a virtualized environment.

This lab was designed to strengthen practical understanding of:

* SIEM deployment and monitoring
* Firewall log analysis
* Threat detection workflows
* Network visibility and traffic control
* Security event correlation
* Defensive security operations

---

# Key Features

* Integrated pfSense firewall logs into Wazuh SIEM
* Configured centralized Syslog monitoring
* Created custom Wazuh decoders for pfSense firewall events
* Developed custom alerting rules for suspicious traffic activity
* Implemented GeoIP traffic filtering using pfBlockerNG
* Enabled DNSBL-based website restriction
* Tested firewall controls and traffic blocking scenarios
* Verified Wazuh Manager, Indexer, and Dashboard services
* Simulated SOC monitoring and alert analysis workflows

---

# Lab Environment

| Component         | IP Address     |
| ----------------- | -------------- |
| pfSense Firewall  | 192.168.10.1   |
| Kali Linux        | 192.168.10.101 |
| Wazuh SIEM Server | 192.168.10.102 |

---

# Technologies Used

* pfSense Community Edition
* Wazuh
* VMware Workstation
* Linux
* Syslog
* pfBlockerNG
* MaxMind GeoIP
* XML Rule & Decoder Configuration

---

# Wazuh Integration

pfSense firewall logs were forwarded to the Wazuh Manager using Syslog over UDP port 514 for centralized monitoring and analysis.

### Wazuh Service Verification

```bash
systemctl status wazuh-manager
systemctl status wazuh-indexer
systemctl status wazuh-dashboard
```

### Restart Service

```bash
systemctl start wazuh-manager
```

---

# Custom Decoder Development

Custom decoders were developed to parse pfSense firewall logs and extract critical network fields:

* Source IP
* Destination IP
* Source Port
* Destination Port

### Decoder Configuration

```xml
<decoder name="pfsense-custom">
  <prematch>filterlog</prematch>
</decoder>

<decoder name="pfsense-fields">
  <parent>pfsense-custom</parent>
  <regex>^.*filterlog:.* (\d+\.\d+\.\d+\.\d+),(\d+\.\d+\.\d+\.\d+),(\d+),(\d+).*$</regex>
  <order>srcip,dstip,srcport,dstport</order>
</decoder>
```

---

# Custom Detection Rules

Created dedicated Wazuh rules to detect:

* Blocked firewall traffic
* Allowed connections
* Repeated deny events
* Suspicious network behavior

### Rule File

```text
pfsense_rules.xml
```

---

# pfBlockerNG Security Controls

Implemented advanced traffic filtering using:

* GeoIP-based country blocking
* Threat intelligence feeds
* DNSBL domain filtering

### Threat Feeds

* Spamhaus DROP
* ET Block
* Abuse_Feodo_C2
* CINS Army

### GeoIP Policy

Configured regional traffic restrictions using:

```text
Deny Both
```

to block both inbound and outbound communication.

---

# DNSBL Website Filtering

Restricted access to selected platforms through DNSBL:

```text
facebook.com
instagram.com
youtube.com
googlevideo.com
```

---

# Firewall Testing & Validation

## ICMP Traffic Blocking

Created LAN firewall rules to block ICMP traffic from selected hosts and validated successful packet drops.

## GeoIP Filtering Validation

Performed connectivity tests against blocked regional IPs using curl and ping-based testing methods to verify outbound traffic restrictions.

---

# Skills Demonstrated

* SIEM Administration
* Firewall Configuration
* Log Management
* Threat Detection Engineering
* Security Monitoring
* Network Traffic Analysis
* Rule & Decoder Development
* SOC Operations Fundamentals
* Defensive Security Practices

---

# Author

## Arshman Abbas

LinkedIn:
[LinkedIn Profile](https://www.linkedin.com/in/arshman-abbas-89a95732a/?utm_source=chatgpt.com)

---

# License

Licensed under the MIT License.







