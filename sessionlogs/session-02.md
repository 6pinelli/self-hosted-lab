# Linux Server, SSH and Basic Administration

Session 2 actioned the following items:

## Installing needed tools:
- Oracle Virtual Box 7.2.8 with dedicated partition assigned to host Virtual Machines
- Virtual Ubuntu Machine on Virtual Box (virtual machine support must be enabled in BIOS): <br>
  Ubuntu 26.04 LifeServer AMD64 with 4096 MB Memory, 4 CPUs, 25 GB Disk in Bridged Mode\

  <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/02-01-installUB.jpg" alt="Ubuntu Install 1" width="500">
  <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/02-02-installUB.jpg" alt="Ubuntu Install RAMCPU" width="500">
  <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/02-03-installUB.jpg" alt="Ubuntu Install BridgeAdapter" width="500">

  Create credentials:\
  <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/02-04-installUB.jpg" alt="Ubuntu Install Credentials" width="600">
\
  (Once installed, reboot machine, log in with created credentials)



 - Determine assigned IP address for SSH access - type in server machine
```
   ip a
```
<br>
    <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/02-05-ip.jpg" alt="ip a" width="500">



## Accesse Ubuntu Server for basic setup and first steps via SSH from Host Terminal

Update Ubuntu to most recent versions:

- Get list of all available updates:
```
sudo apt update
```
- Confirm and upgrade system to all available updates with option -y \
  (will confirm upgrade requests with yes for all available updates)
```
sudo apt upgrade -y
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
   <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/02-06-whoami.jpg" alt="whoamihostname" width="400">
   <i>here:</i> username: labuser, host: ubuntu-lab

<br>
<br>

- Determine available disk space:<br>
  (disk free -humanreadable)<br>

```
df -h
```
   <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/02-07-df.jpg" alt="Disk Free" width="500">
<br>
   <i>here:</i> device "sda2" has a total capacity of 25 GB of which 6.8 GB are used and 17 GB are available (30% used)
  
<br>
<br>

- Determine memory usage (RAM - h for human readable):<br>

```
free -h
```
   <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/02-08-free.jpg" alt="Free" width="500">
<br>
   <i>here:</i> 3.3 Gi total RAM, thereof 2.1 Gi unused (free)
  
<br>
<br>


- Query system log entries (here the last 20)
```
sudo journalctl -n 20
```
Output will read: Date, Time, Hostname, Process/Service Name, Process ID, Message

   <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/02-09-journal.jpg" alt="System Logs" width="500">
<br>

