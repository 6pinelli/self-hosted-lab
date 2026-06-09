# Docker, First Container Install: NGINX

Session 3 actioned the following items:

## Installing Docker:
- Installing Docker, a containerization platform will package applications into isolated units (= containers).
- This will prevent conflicts between applications, efficiency and offer portability if needed.
- Docker Hub is a trusted source for app images/blueprints.

1) Update Ubuntu if need be
```
  sudo apt update
  sudo apt upgrade -y
```

2) With first installation on machine, create repository to receive always newest updates directly from docker
```
# Add Docker's official GPG key:
  sudo apt update
  sudo apt install ca-certificates curl
  sudo install -m 0755 -d /etc/apt/keyrings
  sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
  sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
  sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
  Types: deb
  URIs: https://download.docker.com/linux/ubuntu
  Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
  Components: stable
  Architectures: $(dpkg --print-architecture)
  Signed-By: /etc/apt/keyrings/docker.asc
  EOF

  sudo apt update
```
\
      <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-01-repos1.png" alt="Docker Install 1" width="600">\
      <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-02-repos2.png" alt="Docker Install 2" width="600">

(source: <a href="https://docs.docker.com/engine/install/ubuntu" >Docker Installation Instructions</a>)

3) Install Docker:
```
  sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
  This will install directly from Docker, not Ubuntu's repositories and offer better support (regular updates)
<br>
    <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-03-dockinstall.png" alt="Docker Install 3" width="600">
    
- Verification of installation shows docker is installed and running:
```
  # Active status shows docker is running

  sudo systemctl status docker
```
<br>      <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-04-systemctl.png" alt="Docker Status" width="600">
    
```
# Below command will show successful intallation by downloading a test image, running it in a container, and thereafter printing a confirmation message and exits

  sudo docker run hello-world
```
<br>      <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-05-helloworld.png" alt="Docker Hello World" width="600">



## Deploy NGINX

NGINX is an open-source software for webservers with funtions including reverse proxy, load balancing and HTTP caching.

1) Install:
```
  docker pull nginx
```
<br>    <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-06-pullnginx.png" alt="Pull NGINX" width="600">


2) Run NGINX:
```
  docker run -d -p 8080:80 nginx
```
<br>    <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-06-runapp.png" alt="Run NGINX" width="600">


3) Verify app is running

- Method 1 "process status request":
```
  docker ps
```
<br>
  The image below shows the output. NGINX container is running with the container ID a3aa5e87116e having been created from the nginx image.<br>
  It reflects the command that running inside the container next, followed by creation time, current status, port mapping and the auto-generated name for the container.
 <br>   <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-07-dockerps.png" alt="DockerPS" width="700">
<br>
<br>
- Method 2: access app in browser via IP and port: App showing and running confirmed
<br>    <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-08-browsertest.png" alt="browsertest" width="600">
<br>

4) Inspect an app

- Logs can per app can be requested showing each process for the app:
  The log will show time stamp of when the entry was generated, log level (severity, i.e. info, error, warning...), message containing the actual content as well as at times the source of the app generating the log.
```
  docker logs a3aa5e87116e
  #syntax: docker logs [container ID]
```
<br>    <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-09-dockerlogs.png" alt="Docker Logs" width="600">
<br>

5) Stop and remove a container

- to stop a container from running, use:
```
  docker stop a3aa5e87116e
  #syntax: docker stop [container ID]
```
 <br>   <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-10-dockerstop.png" alt="Docker Stop" width="500">
    
- Verify in browser: app is unavailable and has stopped
<br>    <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-11-dockerstopverify.png" alt="docker stop verification" width="500">
    
<i> Each time, a container session is started, a new container ID will be created, taking up space.
   It is recommended to remove container IDs (unless keeping for trouble shooting logs) to release the space. </i>

- Remove Container Space (rm = remove):
```
  docker rm a3aa5e87116e
  #syntax: docker rm [container id]
```
<br>    <img src="https://github.com/6pinelli/self-hosted-lab/blob/main/screenshots/03-12-dockerrm.png" alt="docker remove" width="600">
