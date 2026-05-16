# Linux Command Reference

## Network Commands


### Check IP address
```bash
ip a
```
Shows all network interfaces and their IP addresses.
Used to find which IP was assigned to each VM.


### Set static IP manually (temporary)
```bash
sudo ip link set enp0s8 up
sudo ip addr add 192.168.178.10/24 dev enp0s8
```
Brings up a network interface and assigns it a static IP.
Temporary — resets on reboot.


### Make static IP permanent (netplan)
```bash
sudo nano /etc/netplan/50-cloud-init.yaml
sudo netplan apply
```
Edits the netplan config file to persist IP across reboots.


### Test connectivity
```bash
ping 192.168.178.10
```
Sends ICMP packets to verify two machines can reach each other.


### Check open ports and services
```bash
nmap -sV 192.168.178.20
```
Scans target IP for open ports and service versions.
-sV flag enables version detection.


## SSH Commands


### Connect to Ubuntu server
```bash
ssh omkar@192.168.178.10
```
Opens SSH session to Ubuntu Wazuh server from Windows PowerShell.


### Connect to old system with legacy key
```bash
ssh -oHostKeyAlgorithms=+ssh-rsa msfadmin@192.168.178.30
```
Required for Metasploitable2 — forces acceptance of old RSA key type.


### Copy file to remote machine
```bash
scp -oHostKeyAlgorithms=+ssh-rsa file.deb msfadmin@192.168.178.30:/home/msfadmin/
```
Securely copies a file from local machine to remote machine.
Used to transfer Wazuh agent deb to Metasploitable.


## System Commands


### Update and upgrade packages
```bash
sudo apt update && sudo apt upgrade -y
```
Updates package list and upgrades all installed packages.
Run this first on any fresh Ubuntu install.


### Check service status
```bash
sudo systemctl status wazuh-manager
sudo systemctl status ssh
```
Shows whether a service is running, stopped, or failed.


### Start and enable service
```bash
sudo systemctl start ssh
sudo systemctl enable ssh
```
Start starts the service now.
Enable makes it start automatically on reboot.


## Wazuh Commands


### Install Wazuh all-in-one
```bash
sudo bash wazuh-install.sh -a -i
```
-a installs all components (manager, indexer, dashboard)
-i ignores OS compatibility check (needed for Ubuntu 24.04)


### Overwrite existing Wazuh install
```bash
sudo bash wazuh-install.sh -a -i -o
```
-o flag wipes existing installation and starts fresh.
Used when a previous install was incomplete.


### Start Wazuh manager
```bash
sudo systemctl start wazuh-manager
sudo systemctl status wazuh-manager
```