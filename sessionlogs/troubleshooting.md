# Troubleshooting throughout all sessions

## Session 03

1) IP address changes making SSH difficult
  IP address can change when virtual machine is used with DHCP
  Either verify IP with every login, or set up static IP:

  1.1) DHCP reservation on router:
     log into router admin, find DHCP reservations or static leases, and bind VM MAC address to static IP

  1.2) Netplan static IP on the M

```
     sudo nano /etc/netplan/00-installer-config.yaml

    # change dhcp4 from true to no and add:
      addresses: [add ipv4 with cidr notation]
      gateway4: [default gateway]
      nameservers:
      addresses: [default DNS server ipv4 devided with comma]

    # press ctrl + x on keyport to exit, save changes with y

sudo netplan apply
```


2) System time in logs unclear
   request system time zone with:

```
   timedatectl
```
<img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-systemtimezone.png" alt="timezone" width="600">


3) Change settings to have to avoid working with sudo command all the time:

  ```
   sudo usermod -aG docker $USER
   newgrp docker
   groups
```
   This will will modify the user account settings (usermod)  to append (-a) a user to the docker group (-G) and expand it to the currend username ($USER).
   The Docker daemon runs with root privileges - only members of the docker group can communicate with it without sudo.
   newgrp docker will activate the docker group membership in your current terminal session to avoid log out and in again
   Groups command will verify to show the docker group now.

<img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-sudoall.png" alt="Sudo all" width="600">


4) Typos
   Many errors simply occur due to typos - below example:
   docker pull ngNIx instead of docker pull ngINx

<img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-typo.png" alt="Sudo all" width="600">
