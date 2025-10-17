# Nessus (Essentials) Vulnerability Scanning Lab

## Overview

This project documents a vulnerability assessment performed from a local host (Nessus running locally) against a single Windows 10 virtual machine configured on a Host‑Only network. The goal is to discover, analyze, and remediate vulnerabilities and to produce evidence and a short remediation plan suitable for a portfolio or resume.

---

## Lab Topology

* **Host:** Your personal machine running Nessus (Essentials or Pro)
* **Target:** Windows 10 VM (Host‑Only network)
* **Virtualization:** VirtualBox
* **Network:** Host‑Only adapter (isolated)

---

## Quick Start

1. Configure a Host‑Only network in VirtualBox/VMware and attach the Windows 10 VM.
2. Install Nessus Essentials on your host and register/activate it.
3. Create a Basic Network Scan in Nessus targeting the VM IP.
4. Add SMB/WinRM credentials (local admin account) and run a credentialed scan.
5. Export reports (PDF / CSV), capture screenshots.

---

## Images / Screenshots (placeholders)

Use these image filenames when adding screenshots to the `images/` folder in your repo.

* `images/vm_network_config.png` — VM network settings showing Host‑Only adapter and IP.
* `images/nessus_dashboard.png` — Nessus web UI / dashboard.
* `images/basic_scan_summary.png` — Summary of Basic (unauthenticated) scan results.
* `images/credentialed_scan_summary.png` — Summary of credentialed scan results.
* `images/vulnerability_detail.png` — Example vulnerability detail page (plugin, CVE, remediation).
* `images/remediation_evidence.png` — Evidence of remediation (Get‑HotFix output, Windows Update showing KB installed, PowerShell commands, etc.).
* `images/rescan_summary.png` — Post‑remediation re‑scan summary.

---

## **Procedures:**

### 1) Environment setup

* Create a Host‑Only network adapter in VirtualBox/VMware.
* Install or provision a Windows 10 VM and attach it to the Host‑Only adapter.
* Create a local admin account for scans (example: `labadmin` / `P@ssw0rd!`).
* Confirm VM IP with `ipconfig` (e.g., `192.168.56.101`).

> *Image:* `![VM Network Configuration](images/vm_network_config.png)`

### 2) Install & configure Nessus

* Install Nessus on the host and complete activation.
* Open `https://localhost:8834` and finish setup.

> *Image:* `![Nessus Dashboard](images/nessus_dashboard.png)`

### 3)Run Basic Network Scan

* Create a *Basic Network Scan* targeting the VM IP.
* Launch scan; review open ports and service banners.

> *Image:* `![Basic Scan Summary](images/basic_scan_summary.png)`

### 4)Configure Credentials & Run Credentialed Scan

* In Nessus, add Windows credentials (SMB/WinRM) using the local admin account.
* Create a new scan that uses these credentials and run it.

> *Image:* `![Credentialed Scan Summary](images/credentialed_scan_summary.png)`

### 5) Analyze Findings

* Record counts by severity (Critical / High / Medium / Low).
* For top findings, capture plugin ID, CVE, affected component, and recommended remediation.

> *Image:* `![Vulnerability Detail](images/vulnerability_detail.png)`


---

## Example Finding (copy into your report and edit)

**Title:** SMBv1 Protocol Enabled

**Severity:** High

**Description:** SMBv1 is an outdated and insecure protocol known to be vulnerable to remote code execution exploits (e.g., EternalBlue). It should be disabled on modern systems.

**Remediation:** Run PowerShell as Administrator:

```powershell
Disable-WindowsOptionalFeature -Online -FeatureName smb1protocol
Restart-Computer
```

**Verification:** Re-scan with Nessus and confirm the SMBv1 plugin no longer appears.

---

## Example Write‑Up (paste into your portfolio)

> **Nessus Vulnerability Assessment — Windows 10 (Host‑Only Lab)**
>
> Conducted vulnerability assessments using Tenable Nessus Essentials from my local host against an isolated Windows 10 VM. Performed both unauthenticated and credentialed SMB/WinRM scans to identify network‑facing and host‑level vulnerabilities. Prioritized findings by CVSS and exploitability, implemented remediation (Windows updates, removing insecure shares, adjusting NTFS permissions), and validated fixes via re‑scan. Exported findings as PDF and CSV and documented remediation steps.

**Key metrics (replace with your results):**

* Critical: 0
* High: 2
* Medium: 5
* Low: 8

**Outcome:** Reduced high severity findings by 100% after applying patches and configuration changes (re-scan validated).

---

## Repo Structure

```
Nessus-Vulnerability-Scan/
├─ images/
│  ├─ vm_network_config.png
│  ├─ nessus_dashboard.png
│  ├─ basic_scan_summary.png
│  ├─ credentialed_scan_summary.png
│  ├─ vulnerability_detail.png
│  ├─ remediation_evidence.png
│  └─ rescan_summary.png
├─ remediation_plan.md
└─ README.md
```

---

## Resume Bullet (copy & edit)

* Executed Nessus vulnerability scans (unauthenticated + credentialed) against an isolated Windows 10 lab VM; analyzed findings, prioritized remediation by CVSS, implemented fixes, and validated remediation via re-scan.

---

## License

This project is provided for educational purposes. Replace / add a license as desired.

---

*Generated README template — add your screenshots to `images/` and replace placeholder counts and KB numbers with your lab results before publishing.*
