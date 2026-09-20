# SOC Detection Lab - Splunk

A hands-on SOC lab simulating reconnaissance and SSH brute-force attacks and detecting them using Splunk SIEM.

---

## Overview

This lab demonstrates how a SOC analyst can detect and investigate malicious activity using Splunk SIEM.

The simulated attack chain included:

- Reconnaissance using Nmap
- SSH brute-force attacks using Hydra
- Log collection and monitoring in Splunk
- Detection through SPL queries
- Investigation and evidence analysis

---

## Lab Environment

- Kali Linux
- Nmap
- Hydra
- Splunk SIEM
- Target Machine

---

## Lab Overview

images/01-lab-overview.png

---

## Attack Scenario

The attack environment consisted of:

- Kali Linux (Attacker)
- Victim Machine
- Splunk SIEM

images/02-attack-scenario.png

---

## Phase 1 - Reconnaissance

The attacker performed host discovery and service enumeration.

images/03-reconnaissance-phase.png

### Objectives

- Identify active hosts
- Discover open ports
- Detect running services

---

## Phase 2 - SSH Brute Force Attack

Hydra was used to launch multiple authentication attempts against the SSH service.

images/04-bruteforce-phase.png

### Objectives

- Test credentials
- Simulate unauthorized access attempts
- Generate security events for analysis

---

## Blue Team Detection

Splunk collected logs generated during the attack.

images/05-detection-telemetry.png

Detection focused on:

- Port scanning activity
- Failed logons
- Successful authentication following multiple failures

---

## SPL Query – Brute Force Detection

```spl
sourcetype=linux_secure "Failed password"
| stats count by src_ip, user
| where count > 10
```

images/06-bruteforce-query.png

---

## SPL Query – Port Scan Detection

```spl
sourcetype=ids OR firewall
| stats dc(dest_port) as unique_ports by src_ip
| where unique_ports > 15
```

images/07-portscan-query.png

---

## Real Evidence – Reconnaissance Activity

Actual screenshot captured during reconnaissance.

images/08-real-reconnaissance-evidence.png

---

## Real Evidence – Splunk Analysis

Actual Splunk screenshots showing event analysis.

images/09-real-splunk-detection.png

---

## Additional Investigation Evidence

Victim IP verification and event volume analysis.

images/10-target-and-detection-evidence.png

---

## SOC Analyst Perspective

### Indicators Observed

- Port scanning activity
- High connection volume
- Multiple failed SSH logins
- Successful login after repeated failures
- Significant increase in event volume

### Potential Alerts

- Port Scan Alert
- SSH Brute Force Alert
- Suspicious Authentication Alert
- Excessive Failed Login Alert

---

## Skills Demonstrated

- Network Reconnaissance
- Nmap Enumeration
- Hydra Usage
- Splunk SIEM
- Log Analysis
- Security Monitoring
- Threat Detection
- Alert Development
- SOC Investigation

---

## Key Takeaways

- Security monitoring provides visibility across the attack lifecycle.
- Reconnaissance activity can be detected before compromise.
- Failed authentication events are valuable indicators of attack activity.
- SPL queries can be used to rapidly identify malicious behavior.
- Centralized logging enables efficient incident investigation.

---

## Full Report

The complete lab report is available in:

`SOC-Detection-Lab.pdf`
