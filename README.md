<div align="center">

# 🕵️ Red Team Operations Simulation — Mr. Robot VM

### Full-Chain Attack Lifecycle Report

**Ethical Hacking Fundamentals — Spring Semester 2026**

[Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)
[Environment](https://img.shields.io/badge/Environment-Isolated%20Lab-blue?style=flat-square)
[Target](https://img.shields.io/badge/Target-VulnHub%20Mr.%20Robot-critical?style=flat-square)

</div>

---

## 📌 Overview

This repository documents a **controlled, authorized penetration test** performed against the *Mr. Robot* virtual machine ([VulnHub](https://www.vulnhub.com/)) as the course project for **Ethical Hacking Fundamentals**.

The engagement was conducted entirely inside an **isolated VMware laboratory environment** with no external network access, following a structured five-stage attack lifecycle:

1. 🔍 Reconnaissance
2. 🛰️ Scanning & Enumeration
3. 🔓 Gaining Access
4. ⬆️ Post-Exploitation & Privilege Escalation
5. 🧹 Post-Exploitation Analysis & Cleanup

The engagement resulted in **full compromise of the deliberately vulnerable target machine**, with the complete attack chain documented in the accompanying assessment report.

---

## 👥 Team

| Role | Name | Student ID | Responsibility |
|------|------|------------|----------------|
| The Scout | Mohamed Ali Ali Dabash | 202505177 | Reconnaissance, scanning & enumeration, initial web analysis |
| The Ghost | **Ahmed Amir Ibrahim** | 202507440 | Exploitation, post-exploitation, privilege escalation, forensic analysis & cleanup |

---

## 🖥️ Lab Environment

| Component | Detail |
|-----------|--------|
| Hypervisor | VMware Workstation |
| Network | Isolated VMware NAT laboratory network |
| Attacker | Kali Linux |
| Target | Mr. Robot — VulnHub (Intermediate) |

> **Note:** The original target, Kioptrix Level 2, failed to initialize correctly in the laboratory environment. After troubleshooting the network configuration, the team switched to the Mr. Robot VM, which was confirmed reachable and suitable for the assessment.

---

## 🧭 Attack Chain Summary

| Phase | Action | Key Tool(s) | Outcome |
|-------|--------|-------------|---------|
| Recon | Host discovery | `nmap -sn` | Target identified |
| Scanning | Service/version scan | `nmap -sV -sC -A` | Web services and software versions identified |
| Scanning | Web vulnerability scan | Nikto | Outdated software and missing security headers identified |
| Scanning | Robots.txt review | `curl` | Sensitive files and application information discovered |
| Scanning | CMS enumeration | WPScan | WordPress version, configuration and attack surface identified |
| Access | Credential attack | WPScan + wordlist | Valid administrative credentials discovered |
| Access | Admin dashboard login | Browser | Administrative access obtained |
| Access | Reverse shell | Theme Editor + Netcat | Initial shell obtained as a low-privileged user |
| Post-Exploit | Sensitive file discovery | `ls` / `find` | Password hash and protected files identified |
| Post-Exploit | Hash analysis | `john` | Weak password recovered |
| Post-Exploit | Privilege pivot | `su` | Access to a higher-privileged user obtained |
| Privilege Escalation | SUID binary enumeration | `find -perm -4000` | Vulnerable SUID Nmap installation identified |
| Privilege Escalation | Root access | Nmap interactive mode | Full system compromise achieved |
| Forensics | Log analysis | `cat` / `grep` | Attack activity and authentication events reviewed |
| Cleanup | Artifact removal | System administration tools | Lab environment restored after assessment |

---

## 🐛 Vulnerabilities Identified & Remediated

| # | Vulnerability | Severity | Fix Summary |
|---|---------------|----------|-------------|
| 1 | Outdated WordPress (4.3.1) | 🔴 Critical | Update to a supported stable release |
| 2 | Weak administrative credentials | 🔴 Critical | Enforce strong passwords + 2FA |
| 3 | XML-RPC Multicall brute-force exposure | 🟠 High | Disable `xmlrpc.php` when unnecessary |
| 4 | Theme/Plugin Editor code execution | 🔴 Critical | Disable file editing in WordPress configuration |
| 5 | Unsalted MD5 password storage | 🟠 High | Use modern salted password hashing |
| 6 | SUID bit on legacy Nmap 3.81 | 🔴 Critical | Remove unnecessary SUID permissions and upgrade Nmap |
| 7 | End-of-life PHP 5.5.29 | 🟠 High | Upgrade to a supported PHP version |
| 8 | Missing HTTP security headers | 🟡 Medium | Add CSP, HSTS, X-Frame-Options, and related headers |

---

## 🧰 Tools Used

`Nmap` · `Nikto` · `Gobuster` · `WPScan` · `curl` / `wget` · `Netcat` · `John the Ripper` · `Python`

---

## 🛠️ Troubleshooting Log

The assessment documents **6 troubleshooting incidents** encountered and resolved during the engagement, including:

- Network initialization issues with the original target VM
- Shell parsing errors
- Directory enumeration timeouts
- Incorrect tool flag syntax
- Failed file downloads
- A corrupted wordlist affecting credential testing

Each incident is documented in the full report with its **root cause, troubleshooting process, and resolution**.

---

## 📂 Repository Contents

| File | Description |
|------|-------------|
| `Red_Team_Report_MrRobot.pdf` | Full assessment report — methodology, technical analysis, evidence, troubleshooting, remediation, and appendix |

---

## ⚠️ Disclaimer

This assessment was conducted strictly against a **deliberately vulnerable, publicly available training VM (VulnHub — Mr. Robot)** inside an **isolated laboratory environment** for academic purposes only.

No techniques described in this project were used against systems without explicit authorization.

This repository is intended for **educational and defensive security purposes only**.

---

<div align="center">

**Course:** Ethical Hacking Fundamentals · Spring 2026

</div>
