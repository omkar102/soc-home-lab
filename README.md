# soc-home-lab

A personal cybersecurity home lab built for soc analyst and dfir skill development.

# objective

Practical real-world blue team skills including:
- Log analysis and SIEM monitoring
- Alert triage and investigation
- Attack simulation and detection
- Incident documentation

# lab architecture

- Windows 11 Host (192.168.178.1): Analyst machine + monitored endpoint.
- Ubuntu Server 24.04 (192.168.178.10): Wazuh SIEM Manager.
- Metasploitable 2 (192.168.178.30): Vulnerable Linux target.
- Windows 10 VM (192.168.178.20): Primary victim/monitored endpoint.
- Kali Linux (): Attacker Machine and DHCP.

# tools installed

- Wazuh 4.7.5 — SIEM and XDR.
- Sysmon + SwiftOnSecurity config — Windows telemetry.
- Wazuh agents — on Windows 11 host and Windows 10 VM.

# network

- All VMs on VirtualBox Host-Only network (192.168.178.x).
- Kali has additional NAT adapter for internet access.

# skills practiced:

- SIEM deployment and configuration.
- Agent-based log collection.
- Windows endpoint monitoring.
- Attack simulation and detection.
- Incident report writing.
