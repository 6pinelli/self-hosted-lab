# Linux Server, SSH and Basic Administration

- Installed Oracle Virtual Box 7.2.8 with dedicated partition to host Virtual Machines
- Installed within Virtual Box simple Ubuntu Server Virtual Machine (virtual machine support must be enabled in BIOS): <br>
  (Ubuntu 26.04 LifeServer AMD64 with 4096 MB Memory, 4 CPUs, 25 GB Disk in Bridged Mode)
 - Once installed, rebooted Machine and logged in with credentials created
 - Check assigned IP address
```
   ip a
```
 - Accessed machine for basic setup and first admin steps via SSH from Host Terminal
 - Updated Ubuntu via SSH:

```
sudo apt update (will give list of available updates)
sudo apt upgrade -y (will upgrade to all available updates)
```
- Confirm User and Hostname working on:
```
whoami (returns user)
hostname (returns machine/host working on)
```

```
df -h
```
```
free -h
```

```
sudo journalctl -n 20
```
