# Linux Server, SSH and Basic Administration

Session 2 actioned the following items:

## Installing needed tools:
- Oracle Virtual Box 7.2.8 with dedicated partition assigned to host Virtual Machines
- Virtual Ubuntu Machine on Virtual Box (virtual machine support must be enabled in BIOS): <br>
  Ubuntu 26.04 LifeServer AMD64 with 4096 MB Memory, 4 CPUs, 25 GB Disk in Bridged Mode\
  (Once installed, rebooted Machine and logged in with credentials created)
 - Determine assigned IP address for SSH access - type in server machine
```
   ip a
```
## Accesse Ubuntu Server for basic setup and first steps via SSH from Host Terminal

Update Ubuntu to most recent versions:

- Get list of all available updates:
```
sudo apt update
```
- Confirm and upgrade system to all available updates with option -y \
  (will confirm upgrade requests with yes for all available updates)
```
sudo apt upgrade -y (will upgrade to all available updates)
```

Testing tools used for troule shooting and baseline:

- Confirm User and Hostname working on:\
Who am I option will return current user name
```
whoami
```
Return name of current machine/host:
```
hostname
```

- Determine available disk space:\
(disk free -humanreadable)
```
df -h
```

- Determine memory usage (RAM - h for human readable):
```
free -h
```

- Query system log entries (here the last 20)
```
sudo journalctl -n 20
```
Output will read: Date, Time, Hostname, Process/Service Name, Process ID, Message
