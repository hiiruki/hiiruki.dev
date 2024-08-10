---
title: "How to Install Docker on Ubuntu 20.04 VPS"
description: "A guide to install Docker on Ubuntu 20.04 VPS"
summary: "This guide will help you to install Docker on Ubuntu 20.04 VPS"
date: 2024-08-09T20:38:13+07:00
draft: false
author: "Hiiruki"
tags: ["docker", "ubuntu", "VPS", "installation", "guide", "linux", "containerization", "container", "virtualization"]
showToc: true
TocOpen: false
TocSide: 'right'
# weight: 1
# aliases: ["/first"]
hidemeta: false
comments: false
disableHLJS: true # to disable highlightjs
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
# UseHugoToc: true
cover:
    image: "images/cover.webp" # image path/url
    alt: "Cover: Zoom Logo" # alt text
    caption: "" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
# editPost:
#     URL: "https://github.com/hiiruki/hiiruki.dev/tree/main/content/blog/install-docker-ubuntu/index.md"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

## Intro

Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker's methodologies for shipping, testing, and deploying code, you can significantly reduce the delay between writing code and running it in production.

## Prerequisites

- A server running Ubuntu 20.04 or later
- A user with sudo privileges

## Development Environment

- Ubuntu 20.04 LTS
- Docker version 27.1.1, build 6312585

## Steps

### Step 1: Installing Docker

The Docker package is included in the default Ubuntu repositories. However, it may not always be the latest version. The recommended approach is to install Docker from the official Docker repository. To do this, we will need to add the Docker repository, the GPG key, and then install the Docker package.

First, update your existing list of packages:

```bash
sudo apt update
```

Install the required packages to allow apt to use a repository over HTTPS:

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

Then add the Docker GPG key:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Add the Docker repository to APT sources:

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Update the package database with the Docker packages from the newly added repository:

```bash
sudo apt update
```

Make sure you are about to install from the Docker repository instead of the default Ubuntu repository:

```bash
apt-cache policy docker-ce
```

You should see output similar to this:

```bash
docker-ce:
  Installed: (none)
  Candidate: 5:27.1.1-1~ubuntu.20.04~focal
  Version table:
     5:27.1.1-1~ubuntu.20.04~focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
     5:27.1.0-1~ubuntu.20.04~focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages

```

![apt cache policy docker-ce](images/apt_cache_policy_docker.webp#center)

> ⓘ NOTE
> <br> Notice that `docker-ce` is not installed, but the candidate for installation is from the Docker repository for Ubuntu 20.04 (focal). The `docker-ce` version number might be different.

Finally, install Docker:

```bash
sudo apt install docker-ce
```

Once the installation is complete, check the version.

```bash
docker --version
```

You should see output similar to this, showing the Docker version number:

```bash
Docker version 27.1.1, build 6312585
```

![docker version](images/docker_version.webp#center)

Now check the status of the Docker service:

```bash
sudo systemctl status docker
```

You should see output similar to this, showing that the service is active and running:

```bash
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2024-08-09 20:00:54 CST; 3h 18min ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 2545366 (dockerd)
      Tasks: 7
     Memory: 35.4M
     CGroup: /system.slice/docker.service
             └─2545366 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

Aug 09 20:00:52 yume systemd[1]: Starting Docker Application Container Engine...
Aug 09 20:00:53 yume dockerd[2545366]: time="2024-08-09T20:00:53.219520920+08:00" level=info msg="Starting up"
Aug 09 20:00:53 yume dockerd[2545366]: time="2024-08-09T20:00:53.233981841+08:00" level=info msg="detected 127.0.0.53 nameserver, assu>Aug 09 20:00:53 yume dockerd[2545366]: time="2024-08-09T20:00:53.587673152+08:00" level=info msg="Loading containers: start."
Aug 09 20:00:54 yume dockerd[2545366]: time="2024-08-09T20:00:54.086716963+08:00" level=info msg="Loading containers: done."
Aug 09 20:00:54 yume dockerd[2545366]: time="2024-08-09T20:00:54.195641146+08:00" level=warning msg="WARNING: No swap limit support"
Aug 09 20:00:54 yume dockerd[2545366]: time="2024-08-09T20:00:54.196219187+08:00" level=info msg="Docker daemon" commit=cc13f95 contai>Aug 09 20:00:54 yume dockerd[2545366]: time="2024-08-09T20:00:54.196382621+08:00" level=info msg="Daemon has completed initialization"
Aug 09 20:00:54 yume dockerd[2545366]: time="2024-08-09T20:00:54.322659066+08:00" level=info msg="API listen on /run/docker.sock"
Aug 09 20:00:54 yume systemd[1]: Started Docker Application Container Engine.
lines 1-21/21 (END)
```

![docker daemon](images/docker_daemon.webp#center)

### Step 2: Using Docker as a Non-Root User (Optional)

By default, Docker requires administrator privileges to run.

when you run the `docker` command, you will get an error like this:

```bash
docker: permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Head "http://%2Fvar%2Frun%2Fdocker.sock/_ping": dial unix /var/run/docker.sock: connect: permission denied.
See 'docker run --help'.
```

![docker: permission denied](images/docker_non_root.webp#center)

To avoid having to use `sudo` with every Docker command, add your user to the Docker group:

```bash
sudo usermod -aG docker ${USER}
```

Then logout and log back in so that your group membership is re-evaluated. or you can run the following command:

```bash
su - ${USER}
```

You will be prompted to enter your user’s password to continue.

or apply the new group membership by running:

```bash
newgrp docker
```

or you can reboot your system:

```bash
sudo reboot
```

Check that your user is now added to the Docker group by running:

```bash
groups
```

or

```bash
id -nG
```

You should see `docker` in the list of groups for your user:

Output:

```bash
hiiruki sudo docker
```

![groups](images/groups.webp#center)

To add another user to the Docker group that you're not currently logged in as, run the following command:

```bash
sudo usermod -aG docker `username`
```

### Step 3: Testing Docker

Now that Docker is installed, let's run a simple container to test it.

Run the following command:

```bash
docker run hello-world
```

If it works, you will see the following output:

```bash
hiiruki@yume:~$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
c1ec31eb5944: Pull complete 
Digest: sha256:1408fec50309afee38f3535383f5b09419e6dc0925bc69891e79d84cc4cdcec6
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

![docker run hello-world](images/docker_run_hello_world.webp#center)

> ⓘ NOTE
> <br> If you see the `Unable to find image 'hello-world:latest' locally` message, it means that the `hello-world` image was not found on your local system. Docker then pulled the image from the Docker Hub, which is the default repository for Docker images.

### Step 4: Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application's services. Then, with a single command, you create and start all the services from your configuration.

Docker Compose is already included in the Docker package that we installed earlier. To check the version, run:

```bash
docker compose version
```

You should see output similar to this, showing the Docker Compose version number:

```bash
Docker Compose version v2.29.1
```

![docker compose version](images/docker_compose_version.webp#center)

#### Operation Check

Now, let's start a web server with nginx to check the operation. Prepare three files: `Dockerfile`, `compose.yaml`, and `src/index.html`

The project structure should look like this:

> ⓘ NOTE
> <br> `composetest` is just an example, you can use any name for the directory.

```bash
composetest/
├── Dockerfile
├── compose.yaml
└── src
    └── index.html
```

Before creating the files, create the `composetest` directory and navigate to it:

```bash
mkdir composetest
cd composetest
```

##### Dockerfile

The image we will use is from the nginx official image [nginx:1.26.1-alpine-slim](https://hub.docker.com/layers/library/nginx/1.26.1-alpine-slim/images/sha256-b13db04c910bbc6a7c9cace95d0029bffc3b9b84670f7136af74f3670b9ef373?context=explore)

Create a file named `Dockerfile`

```bash
nano Dockerfile
```

and add the following content:

```Dockerfile
FROM nginx:1.26.1-alpine-slim
COPY ./src/index.html /usr/share/nginx/html
```

##### compose.yaml

Compose simplifies the control of your entire application stack, making it easy to manage services, networks, and volumes in a single, comprehensible YAML configuration file.

Create a file called `compose.yaml` in your project directory

```bash
nano compose.yaml
```

and paste the following:

```yaml
services:
  nginx:
    build: ./
    image: web-server:1.0.0
    container_name: web-server
    ports:
      - 1337:80
```

Explanation:

This `compose.yaml` file defines a single service named `nginx`. Docker Compose will build a Docker image from the current directory and tag it as `web-server:1.0.0`. It then creates a container named `web-server`, which exposes port `80` of the container to port `1337` on the host machine.

##### src/index.html

Create a directory named `src` and navigate to it:

```bash
mkdir src
cd src
```

create a file named `index.html`:

```bash
nano index.html
```

This is the page that will displayed when you access the web address. For the tutorial, I will use a simple HTML file:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Docker Compose Test</title>
</head>
<body>
    <h1>Hello World!</h1>

    <h2>This file is served by nginx running in a Docker container.</h2>
</body>
</html>
```

##### Build and Run

Now that you have created the necessary files, you can build and run the Docker container using Docker Compose.

Navigate back to the `composetest` directory:

```bash
cd ..
```

Run the following command to build the Docker image and start the container:

```bash
docker compose up -d --build
```

You should see output similar to this:

![docker compose up](images/docker_build.webp#center)

To check the status of the container, run:

```bash
docker ps
```

You should see output similar to this, showing that the container is running:

```bash
CONTAINER ID   IMAGE              COMMAND                  CREATED          STATUS          PORTS                                   NAMES
f3c369713e9f   web-server:1.0.0   "/docker-entrypoint.…"   12 seconds ago   Up 11 seconds   0.0.0.0:1337->80/tcp, :::1337->80/tcp   web-server
```

![docker ps](images/docker_ps.webp#center)

Now, open your web browser and navigate to `http://your_server_ip:port`. You should see the `index.html` page that you created earlier.

![web page](images/web.webp#center)

{{< figure src="./images/containerize.webp" caption="Containerize all the things!" align="center" alt="Containerize all the things!" >}}

## References

- [How To Install and Use Docker on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-22-04)
- [Docker Documentation](https://docs.docker.com/)
- [Docker Compose Quickstart](https://docs.docker.com/compose/gettingstarted/)
- [Ubuntu24.04にDockerをインストールする](https://higmasan.com/docker/install/installing-docker-on-ubuntu24-04/)
