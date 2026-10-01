# Investigation Notes — SSH Brute-Force Detection

## Lab Setup

The project was performed in a controlled VirtualBox environment.

### Systems

- Ubuntu — Splunk Enterprise server
- Kali Linux — SSH log source
- Splunk Universal Forwarder — log forwarding
- VirtualBox — virtualization platform

### Network

Ubuntu / Splunk:

`192.168.56.101`

Kali Linux:

`192.168.56.102`

Splunk receiving port:

`9997`

---

## Log Collection

SSH authentication logs from Kali Linux were collected from the
systemd journal.

The Universal Forwarder was configured to collect events from:

`ssh.service`

The events were forwarded to the Ubuntu Splunk server using TCP 9997.

Sourcetype:

`linux:ssh`

Index:

`main`

---

## Authentication Testing

Controlled SSH authentication attempts were generated between the
Ubuntu and Kali systems.

The investigation produced:

- Multiple failed SSH authentication attempts.
- Three failed attempts from the same source IP.
- Successful authentication events from the same source IP.

---

## Detection Finding

Splunk was used to detect repeated failed SSH authentication attempts.

Detection threshold used in the lab:

`3 or more failed attempts`

Observed source:

`192.168.56.101`

Observed failed attempts:

`3`

---

## Correlation Finding

The failed authentication events were correlated with successful
authentication events.

Observed:

- Failed attempts: `3`
- Successful logins: `2`
- Source IP: `192.168.56.101`

This demonstrated the failed-login followed by successful-login
investigation scenario.

---

## IP Investigation

The source IP was:

`192.168.56.101`

The address was classified as:

`Private / Internal`

The IP belongs to the controlled VirtualBox lab network.

Because the IP is private, public IP reputation was not treated as
meaningful external threat intelligence for this investigation.

---

## Investigation Workflow

The investigation followed:

Log Collection
↓
Detection
↓
Source IP Identification
↓
Authentication Correlation
↓
IP Classification
↓
Analysis
↓
Incident Documentation

---

## Evidence

The following evidence was captured during the project:

- Splunk receiver configuration
- Network connectivity
- Splunk port 9997 listening
- Kali Host-only network configuration
- SSH authentication events
- Source IP correlation
- Private IP classification
- Brute-force detection
- Failed-to-successful authentication correlation

---

## Analyst Observation

The observed authentication activity was generated intentionally
inside a controlled lab environment.

The evidence demonstrates the technical process of detecting and
investigating suspicious SSH authentication activity using Splunk.

It should not be interpreted as a real-world attack against an
external system.