# Pi-hole Docker Compose
Session 4 actioned the following items:

# Preparing Ubuntu

Modern Ubuntu Versions have a build in DNS caching "stub resolver" listening on port 53.
Pi-hole, functioning as DNS sinkhole (blocking of unwanted content such as ads and trackers), would be prevented from listening on port 53.

1) disable stub-resolver
   Create directory for systemd-resolved config overwrites with <i>mkdir -p /etc/systemd/resolved.conf.d</i>
   Create a config file with setting blocking the stub listener with <i>printf "[Resolve]\nDNSStubListener=no\n"</i>
   Writing the setting into a file called <i>no-stub.conf</i> in that directory with <i>| tee /etc/systemd/resolved.conf.d/no-stub.conf</i>.
```
   sudo sh -c 'mkdir -p /etc/systemd/resolved.conf.d && printf "[Resolve]\nDNSStubListener=no\n" | tee /etc/systemd/resolved.conf.d/no-stub.conf'
```

2) Reconfiguring system pointer to new resolver file
   resolv.conf is a file that applications will look in for DNS servers.
   Force remove the existing file with <i>rm -f /etc/resolv.conf</i>
   Creating a symbolic link pointer to the full systemd-resolved resolver config with <i>ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf</i>
   The sysem (apps, containers, ...) will skip the stup and talk to the full resolver which will forwad DNS requests to Pi-hole instead.
```
   sudo sh -c 'rm -f /etc/resolv.conf && ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf'
```

3) Restart resolver to apply above changes
```
   systemctl restart systemd-resolved
```

***** enter image ****

(source: <a href="https://docs.pi-hole.net/docker/tips-and-tricks/" >Pi-hole DNS 53 debug</a>)

# Deploying Pi-hole docker compose

Pi-hole acts as DNS resolver, ad-blocker, tracking blocker,.. - a sinkhole.

1) Create a directory and Docker Compose file:

```
   mkdir ~/pihole                # make directory
   cd ~/pihole                   # change directory into pihole directory
   sudo nano docker-compose.yml  #create docker compose file and write code/directions through nano editor
```
*** image ***


2) Create docker compose - pay attention to spaces and possible typos, see troubleshoot log.
   Important: map http traffic to a different port than 8080 since 8080 was already mapped in nginx docker compose. This would create a conflict for Pi-hole to load and run properly.
```
  services:
    pihole:
      image: pihole/pihole:latest
      container_name: pihole
      ports:
        - "53:53/tcp"
        - "53:53/udp"
        - "8081:80/tcp"
      environment:
        TZ: America/Los_Angeles
        WEBPASSWORD: changeme
        PIHOLE_DNS_1: 1.1.1.1
        PIHOLE_DNS_2: 1.0.0.1
      volumes:
        - ./etc-pihole:/etc/pihole
        - ./etc-dnsmasq.d:/etc/dnsmasq.d
      dns:
        - 8.8.8.8
        - 8.8.4.4
      restart: unless-stopped

```
*** image ***

3) Run docker compose

```
   docker compose up -d
```

*** image ***

   Check if running:
```
   docker compose ps
```

*** image ***
   
# Test functionality of Pi-hole:

1) Access through browser: http://[ip address VM]:8081
   If it loads to a pi-hole login page, Pi-hole is running correctly.

2) Check if legitimate traffic passes through and gets resolved correctly:
```
   nslookup google.com 127.0.0.1
   dig @127.0.0.1 google.com
```
   Correct IP for google.com has been resolved. Dig query came back without any errors.

   *** image ***

3) Check if known spam/tracker/ad domains are blocked: example doubleclick.net
```
   nslookup doubleclick.net 127.0.0.1
```
   Resolves to 0.0.0.0 and ::
   Pi-holes block lists are working. It returns a null address so traffic would immediately fail.

   *** image ***
   


3) 
