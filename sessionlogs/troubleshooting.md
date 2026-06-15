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

<br>   <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-sudoall.png" alt="Sudo all" width="600">


4) Typos <br>
   Many errors simply occur due to typos - below example:
   docker pull ngNIx instead of docker pull ngINx

<br>   <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-typo.png" alt="typos" width="600">


## Session 04 

1) Typos
   Learning curve of mindfulness writing code: spaces and typos can prevent code from being processed correctly. When writing time zones with cities consisting of two words (e.g. Los Angeles): add an underscore between both words.
   
   <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/04-typos1.png" alt="typos1" width="600">
   <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/04-typos2.png" alt="typos2" width="600">

2) DNS conflicts causing gravity databank not loading properly
   With first trial of testing access through browser, it failed. Upon looking at logs, gravity creation failed due to DNS resolution not being available. The logs would get stuck at this point and installation had to be force stopped.
   <br>Gravity database (where the blocklists are saved) would not install.
   ```
   docker compose logs -f
   ```
  <br>   <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/04-dns53.png" alt="DNS" width="600"> 

   Checking which services are listening on port 53, systemd came up. 
   ```
   lsof -i :53
   ```
  <br>   <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/04-lsofi53.png" alt="DNS 53 Listening" width="600">
   
   Solution was eventually found at <a href="https://docs.pi-hole.net/docker/tips-and-tricks/" >Pi-hole DNS 53 debug</a> and implemented (see <a href="https://github.com/6pinelli/self-hosted-lab/blob/main/sessionlogs/session-04.md" >Session Log 04</a>

4) Port conflicts with NGINX
   Anther port conflict was found with NGINX. Since it was also listening on port 8080 for 80 traffic, the solution was to either shut NGINX down or change the listening port for Pi-hole from 8080:80 to 8081:80. Latter was done for an allaround solution where both services can exist if need be.
