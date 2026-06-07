# Linux Server, SSH and Basic Administration

- Installed Oracle Virtual Box 7.2.8 with dedicated partition to host Virtual Machines
- Installed within Virtual Box simple Ubuntu Server Virtual Machine (virtual machine support must be enabled in BIOS): <br>
  (Ubuntu 26.04 LifeServer AMD64 with 4096 MB Memory, 4 CPUs, 25 GB Disk in Bridged Mode)
 - Once installed, rebooted Machine and logged in with credentials created
 - Checked assigned IP address for SSH access with command
```
   ip a
```
 - Accessed machine for basic setup and first admin steps via SSH from Host Terminal

```
# Update Ubuntu to most recent versions:

# To get list of all available updates:
sudo apt update

# Confirm and upgrade system to all available updates with option -y (will confirm upgrade requests with yes for all available updates)
sudo apt upgrade -y (will upgrade to all available updates)

```
```
# Testing tools used for troule shooting and baseline:

# Confirm User and Hostname working on:
# Who am I option will return current user name
whoami

# To see name of current machine/host working on:
hostname

# To see available disk space (e.g. for troubleshooting and baseline creation):
df -h
#(disk free -human readable)

# To see memory usage (RAM - h for human readable):
free -h

# To see system log entries (here the last 20)"
sudo journalctl -n 20

#Output will read: Date, Time, Hostname, Process/Service Name, Process ID, Message
```
