# Day 05 – SOC Tier 1 Incident Report: Linux Log Analysis & File Integrity Monitoring

---

## Incident Summary

- **Incident Type:** Suspicious SSH Activity, Process Monitoring & File Integrity Review
- **Severity:** High
- **Detection Method:** Linux Log Analysis + Process Inspection + File Integrity Checks
- **Tools Used:** SSH, auth.log, last, lastb, ps aux, find
- **Status:** Investigated (Simulated SOC Environment)

---

## Executive Summary

This investigation focuses on identifying unauthorized SSH access attempts, suspicious system activity, and potential persistence behavior on a Linux system.

The analysis includes authentication logs, log history, process monitoring, and file integrity checks to detect possible compromise indicators.

---

## Affected System

- **Operating System:** Kali Linux (Victim Machine)
- **Service Under Investigation:** SSH
- **Log Sources:**
  - `/var/log/auth.log`
  - `last`
  - Process monitoring (`ps aux`)
  - `/etc` directory integrity checks  

---

## Investigation Methodology

---

### 1. Log Directory Overview

![Log Directory](./screenshots/log_directory.png)

- Reviewed Linux log storage structure  
- Identified authentication log locations  
- Confirmed forensic data sources available  

---

## Authentication Log Analysis

---

### 2. Failed & Suspicious Login Attempts

![Auth Logs](./screenshots/auth_logs.png)

- Inspected `/var/log/auth.log`  
- Detected multiple failed SSH login attempts  
- Observed repeated authentication failures from external IP  

### SOC Observations:

- Repeated login attempts indicate brute-force attack  
- Multiple username guessing patterns detected  
- External attacker IP identified  

---

### 3. Login History Review

![Login History](./screenshots/login_history.png)

- Reviewed successful login sessions  
- Checked login timestamps and user activity  
- Identified suspicious access patterns  

### SOC Observations:

- Unusual login attempts flagged  
- Any unknown IP or user is treated as suspicious  

---

## Process Monitoring (System Activity)

---

### 4. Active Process Analysis

![Process Monitoring](./screenshots/ps_ax.png)

- Monitored running system processes using `ps aux` / `ps ax`  
- Identified active processes and execution behavior  
- Checked for suspicious or unknown processes  

### SOC Observations:

- Look for unusual processes such as:
  - unknown binaries
  - suspicious scripts
  - unexpected background services  
- Process anomalies may indicate malware execution  

---

## File Integrity Monitoring

---

### 5. /etc Directory Modifications

![ETC Modified](./screenshots/etc_modified.png)

- Checked recently modified system configuration files  
- Investigated unauthorized system changes  

### SOC Observations:

- Any modification in `/etc` is considered high-risk  
- May indicate system tampering or persistence setup  

---

### 6. Critical System Files Check

![Critical Files](./screenshots/critical_files.png)

- Verified integrity of:
  - `/etc/passwd`
  - `/etc/shadow`

### SOC Observations:

- Changes in authentication files indicate compromise risk  
- Permission or timestamp changes are critical indicators  

---

## Attack Simulation Evidence

---

### 7. Attacker Creation Activity

![Simulation Changes](./screenshots/simulation_changes.png)

- Created test malicious user account  
- Simulated attacker persistence behavior  
- Verified system response to account creation  

### SOC Observations:

- New user creation detected in system logs  
- May indicate attacker attempting persistence  
- Requires immediate investigation in real environment  

---

## Log Validation

---

### 8. Authentication Log Review (Latest Activity)

![Auth Log Tail](./screenshots/auth_log_tail.png)

- Reviewed latest authentication events  
- Traced recent login and system activity  
- Validated brute-force and login behavior  

---

## Indicators of Compromise (IOCs)

- Multiple failed SSH login attempts  
- External IP brute-force activity  
- Successful login anomalies  
- Suspicious system process execution  
- Unauthorized user creation (attacker account)  
- File modifications in `/etc`  
- Authentication log anomalies  

---

## MITRE ATT&CK Mapping

| Behavior              | Technique ID | Description              |
|----------------------|--------------|--------------------------|
| Brute Force Attack   | T1110        | Credential Access        |
| Valid Accounts       | T1078        | Account Access Abuse     |
| Account Creation     | T1136        | Persistence              |
| Process Execution    | T1059        | System Execution         |
| File Modification    | T1112        | System Tampering         |

---

## SOC Analyst Findings

- SSH brute-force attempts confirmed in logs  
- Unauthorized login attempts detected  
- Suspicious process activity observed  
- Attacker account creation simulated successfully  
- File integrity checks show potential system modification  

---

## SOC Analyst Response

- Enforce SSH key authentication  
- Disable root login via SSH  
- Monitor authentication logs continuously  
- Investigate unknown processes immediately  
- Alert on new user creation events  
- Implement file integrity monitoring tools (AIDE / Tripwire)  

---

## Analyst Insight

Linux systems provide strong forensic visibility through logs and process inspection. SOC analysts must correlate authentication activity, process behavior, and file integrity changes to detect compromise attempts effectively.

---

## Learning Outcome

This investigation demonstrates the ability to:

- Analyze Linux authentication logs  
- Detect brute-force SSH attacks  
- Investigate login history  
- Monitor system processes (`ps aux`)  
- Detect unauthorized user creation  
- Identify file integrity violations  
- Simulate attacker behavior in a controlled lab  
- Apply SOC Tier 1 investigation methodology  

---

## Repository Structure

``` id="finalstructurev2"
.
├── README.md
├── screenshots/
│   ├── log_directory.png
│   ├── auth_logs.png
│   ├── login_history.png
│   ├── ps_ax.png
│   ├── etc_modified.png
│   ├── critical_files.png
│   ├── simulation_changes.png
│   └── auth_log_tail.png
````

---

## Conclusion

This investigation demonstrates how Linux systems can be monitored for unauthorized access, malicious process execution, and system tampering. Through structured SOC analysis techniques, early-stage intrusion attempts and persistence behaviors can be effectively detected and mitigated.

```

---
