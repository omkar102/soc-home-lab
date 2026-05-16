# Windows PowerShell Command Reference

## Network Commands

### Check IP configuration
```powershell
ipconfig /all
```
Shows all network adapters, IPs, DNS servers, DHCP status.
Full version of ipconfig with MAC addresses and lease info.


### Set static IP on adapter
```powershell
New-NetIPAddress -InterfaceAlias "Ethernet 2" -IPAddress 192.168.178.20 -PrefixLength 24
```
Assigns static IP to specified network adapter.
PrefixLength 24 = subnet mask 255.255.255.0


### Remove static IP and re-enable DHCP
```powershell
Remove-NetIPAddress -InterfaceAlias "Ethernet" -Confirm:$false
Set-NetIPInterface -InterfaceAlias "Ethernet" -Dhcp Enabled
ipconfig /renew "Ethernet"
```
Removes manually set IP and lets adapter get IP from DHCP automatically.


### Test connectivity
```powershell
ping 192.168.178.10
```
Tests if Windows 10 VM can reach Wazuh server.


### Allow Wazuh through firewall
```powershell
New-NetFirewallRule -DisplayName "Wazuh Agent" -Direction Outbound -Protocol TCP -RemotePort 1514,1515 -Action Allow
```
Opens ports 1514 and 1515 outbound for Wazuh agent communication.


## Sysmon Commands


### Install Sysmon with config
```powershell
.\Sysmon64.exe -accepteula -i sysmonconfig-export.xml
```
Installs Sysmon using SwiftOnSecurity config file.
-accepteula skips license prompt.
-i specifies config file to use.


### Check Sysmon service status
```powershell
Get-Service Sysmon64
```
Confirms Sysmon is running.


## Wazuh Agent Commands


### Install Wazuh agent silently
```powershell
Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.7.5-1.msi -OutFile $env:tmp\wazuh-agent.msi; msiexec.exe /i $env:tmp\wazuh-agent.msi /q WAZUH_MANAGER='192.168.178.10' WAZUH_AGENT_NAME='Windows-10-VM'
```
Downloads and installs Wazuh agent silently.
WAZUH_MANAGER points agent to your Wazuh server IP.
WAZUH_AGENT_NAME sets how it appears in dashboard.


### Start Wazuh agent service
```powershell
NET START WazuhSvc
```
Starts the Wazuh agent Windows service.


### Stop and restart Wazuh agent
```powershell
NET STOP WazuhSvc
NET START WazuhSvc
```
Used after making changes to ossec.conf config file.


### Check Wazuh agent service
```powershell
Get-Service WazuhSvc
```
Confirms agent service is running.


## General Commands


### Check current user
```powershell
whoami
```
Shows current logged in username and domain.
Maps to MITRE T1033 — System Owner/User Discovery.


### List local user accounts
```powershell
net user
```
Lists all local user accounts on the machine.
Maps to MITRE T1087 — Account Discovery.


### Check running processes
```powershell
Get-Process
```
Lists all currently running processes.


### Find files
```powershell
Get-ChildItem -Path C:\ -Recurse -Filter "*.log"
```
Searches recursively for files matching a pattern.