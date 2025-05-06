[Docker]: https://www.docker.com  

# Preparing Docker on a VM with Ubuntu Server 22.04 LTS

>[Docker] is a platform designed to help developers build, share, and run container applications. We handle the tedious setup, so you can focus on the code.

## VM Parameters:
>CPU: 2 vCPU  
RAM: 4096 MB  
Disk: 32 GB

# Install Using the APT Repository

Add Docker's official GPG key:
```sh
sudo apt update && sudo apt upgrade -y
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

Add the repository to APT sources:
```sh
echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu   $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

Install the latest version of Docker:
```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Create the Docker group:
```sh
sudo groupadd docker
```

Add your user to the Docker group:
```sh
sudo usermod -aG docker $USER
```

Activate the group changes:
```sh
newgrp docker
```

Verify that you can run Docker commands without `sudo`:
```sh
docker run hello-world
```
