# Incident Report — SSH Brute-Force Detection

## 1. Incident Summary

A controlled SSH authentication brute-force simulation was performed
in a VirtualBox lab environment.

Splunk detected repeated failed SSH authentication attempts originating
from the same source IP, followed by successful authentication events.

---

## 2. Environment

**SIEM:** Splunk Enterprise

**Log Source:** Kali Linux

**Log Forwarder:** Splunk Universal Forwarder

**Target Service:** SSH

**Source IP:** 192.168.56.101

**Target IP:** 192.168.56.102

---

## 3. Detection

The detection was based on repeated SSH authentication failures.

**Failed SSH Attempts:** 3

**Successful Logins:** 2

The authentication events were collected from the Linux systemd journal
and forwarded to Splunk.

---

## 4. Evidence Observed

The investigation identified:

- Multiple `Failed password` events.
- The same source IP across the failed authentication attempts.
- `Accepted password` events from the same source IP.
- SSH authentication logs successfully forwarded to Splunk.
- The source IP was identified as a private/internal address.

---

## 5. Source IP Investigation

**Source IP:** 192.168.56.101

**Classification:** Private / Internal

The observed IP address belongs to the private lab network.

Because this was a controlled lab environment using a private IP,
public IP reputation was not considered meaningful for determining
whether the address was externally malicious.

---

## 6. Authentication Timeline

The investigation observed multiple failed SSH authentication attempts
followed by successful authentication from the same source IP.

The Splunk investigation showed:

**Source IP:** 192.168.56.101

**Failed Attempts:** 3

**Successful Logins:** 2

---

## 7. Analysis

The repeated failed authentication attempts followed by successful
authentication indicate suspicious authentication activity within the
controlled laboratory environment.

The activity was intentionally generated for security monitoring and
detection practice.

Therefore, this project demonstrates a simulated brute-force detection
scenario rather than a real-world attack.

---

## 8. SOC Investigation Process

The investigation followed this workflow:

Log Collection  
↓  
Authentication Monitoring  
↓  
Repeated Failed Login Detection  
↓  
Source IP Identification  
↓  
Failed + Successful Login Correlation  
↓  
IP Classification  
↓  
Investigation  
↓  
Incident Documentation

---

## 9. Recommended SOC Response

In a real production environment, a SOC analyst could:

- Validate whether the source IP belongs to an authorized system.
- Review the affected user account.
- Review additional authentication activity.
- Investigate activity after the successful login.
- Review endpoint and network telemetry.
- Apply appropriate account protection measures if unauthorized access
  is confirmed.
- Document and preserve relevant evidence.

---

## 10. Conclusion

The project successfully demonstrated a SOC investigation workflow using
Splunk.

The investigation collected Linux SSH authentication logs, detected
repeated failed login attempts, identified the source IP, correlated
failed attempts with successful authentication, classified the IP as
private/internal, and documented the findings in an incident report.

This project provided practical experience with Splunk, SPL, Linux
authentication logs, log forwarding, event correlation, detection, and
SOC incident documentation.

---

## 11. Tools Used

- Splunk Enterprise
- Splunk Universal Forwarder
- Kali Linux
- Ubuntu Linux
- OpenSSH
- Linux systemd journal
- Splunk Processing Language (SPL)
- VirtualBox

---

## 12. Evidence

Supporting evidence is available in the project's `screenshots/`
directory.

The screenshots document:

- Splunk receiver configuration
- Network connectivity
- Splunk port 9997
- Kali SSH authentication logs
- Source IP correlation
- IP classification
- Brute-force detection
- Failed-to-successful authentication correlation