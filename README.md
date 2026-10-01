# SSH Brute-Force Detection using Splunk

## Project Overview

This project demonstrates a hands-on SOC investigation for detecting repeated SSH authentication failures using Splunk.

The lab was built using Kali Linux, Ubuntu, Splunk Enterprise, and Splunk Universal Forwarder.

The objective was to collect SSH authentication logs, detect repeated failed login attempts, identify the source IP, correlate failed attempts with successful authentication, investigate the IP, and document the findings.

## Objectives

- Collect Linux SSH authentication logs
- Forward logs from Kali Linux to Splunk
- Detect repeated failed SSH login attempts
- Identify the source IP address
- Correlate failed and successful authentication events
- Classify the source IP
- Perform basic threat-intelligence assessment
- Create an incident report

## Lab Architecture

Kali Linux
↓
Splunk Universal Forwarder
↓
TCP 9997
↓
Ubuntu / Splunk Enterprise
↓
Detection → Investigation → Correlation → Reporting

## Technologies Used

- Splunk Enterprise
- Splunk Universal Forwarder
- Kali Linux
- Ubuntu Linux
- SSH / OpenSSH
- Linux systemd journal
- Splunk Processing Language (SPL)
- VirtualBox

## Network Configuration

| Component | IP Address | Purpose |
|---|---|---|
| Ubuntu / Splunk | 192.168.56.101 | Splunk server |
| Kali Linux | 192.168.56.102 | SSH log source |
| Splunk Receiver | TCP 9997 | Log receiving |

## Log Collection

SSH authentication logs were collected from the Kali Linux systemd journal and forwarded to Splunk using the Splunk Universal Forwarder.

The configured sourcetype was:

`linux:ssh`

The Splunk receiver was:

`192.168.56.101:9997`

## Detection

The project detected repeated SSH authentication failures from the same source IP.

The investigation identified:

- Source IP: `192.168.56.101`
- Failed SSH attempts: `3`
- Successful logins: `2`
- IP classification: Private / Internal
- Target service: SSH

## Investigation

The investigation correlated multiple failed SSH authentication attempts with subsequent successful authentication events from the same source IP.

Because this was a controlled VirtualBox lab, the observed activity was simulated for defensive security training.

## Evidence

The `screenshots/` directory contains evidence of:

1. Splunk receiver configuration
2. Kali-to-Splunk connectivity
3. Splunk port 9997 listening
4. Host-only network configuration
5. Ubuntu network configuration
6. Kali network configuration
7. Kali Host-only IP
8. SSH authentication events
9. Source-IP correlation
10. IP classification
11. Brute-force detection
12. Failed-to-successful login correlation

## Incident Report

The detailed investigation report is available in:

`reports/incident-report.md`

## Key Learning Outcomes

Through this project, I learned how to:

- Configure Splunk as a SIEM
- Configure a Splunk Universal Forwarder
- Collect Linux authentication logs
- Write SPL queries
- Detect repeated authentication failures
- Extract and investigate source IP addresses
- Correlate authentication events
- Perform basic IP investigation
- Document security findings
- Follow a SOC investigation workflow

## Disclaimer

This project was performed in a controlled VirtualBox lab environment for educational and defensive security purposes.

No external systems were targeted.