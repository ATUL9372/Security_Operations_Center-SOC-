# Docker Installation Guide

Instructions for installing Docker Engine on **Ubuntu**, **Debian**, **Kali Linux**, and **CentOS**.

> Run all commands with `sudo` or as root. After installation, log out and back in (or run `newgrp docker`) for group changes to take effect.

---

## Table of Contents

- [Ubuntu](#ubuntu)
- [Debian](#debian)
- [Kali Linux](#kali-linux)
- [CentOS](#centos)
- [Uninstall](#uninstall)

---

## Ubuntu

### 1. Remove old versions
```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
```

### 2. Set up the repository
```bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
```

### 3. Install Docker Engine
```bash
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### 4. Start and enable the Docker service
```bash
sudo systemctl start docker
sudo systemctl enable docker
```

### 5. Run Docker without `sudo`
```bash
sudo groupadd docker          # skip if the group already exists
sudo usermod -aG docker $USER
newgrp docker
```

### 6. Verify Installation
```bash
docker --version
docker compose version
sudo docker run hello-world
```

You should see a message confirming that Docker is installed and working correctly.


### 7. All in one 
```
sudo apt-get remove docker docker-engine docker.io containerd runc

sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo systemctl start docker
sudo systemctl enable docker

sudo groupadd docker          # skip if the group already exists
sudo usermod -aG docker $USER
newgrp docker

docker --version
docker compose version
sudo docker run hello-world
```

---

## Debian

### 1. Remove old versions
```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
```

### 2. Set up the repository
```bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
```

### 3. Install Docker Engine
```bash
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### 4. Start and enable the Docker service
```bash
sudo systemctl start docker
sudo systemctl enable docker
```

### 5. Run Docker without `sudo`
```bash
sudo groupadd docker          # skip if the group already exists
sudo usermod -aG docker $USER
newgrp docker
```

### 6. Verify Installation
```bash
docker --version
docker compose version
sudo docker run hello-world
```

You should see a message confirming that Docker is installed and working correctly.

---

## Kali Linux

Kali is Debian-based, but its own repos can lag or conflict with Docker's repo. The most reliable approach is to use the **Debian bookworm** Docker repository directly.

### 1. Remove old versions
```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
```

### 2. Install prerequisites and Docker's GPG key
```bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

### 3. Add the Debian (bookworm) repository
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  bookworm stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
```

### 4. Install Docker Engine
```bash
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

> If `apt-get update` errors on the Docker repo, ensure Kali is up to date first (`sudo apt-get update && sudo apt-get dist-upgrade`) and confirm your architecture with `dpkg --print-architecture`.

### 5. Start and enable the Docker service
```bash
sudo systemctl start docker
sudo systemctl enable docker
```

### 6. Run Docker without `sudo`
```bash
sudo groupadd docker          # skip if the group already exists
sudo usermod -aG docker $USER
newgrp docker
```

### 7. Verify Installation
```bash
docker --version
docker compose version
sudo docker run hello-world
```

You should see a message confirming that Docker is installed and working correctly.

---

## CentOS

### 1. Remove old versions
```bash
sudo yum remove -y docker docker-client docker-client-latest docker-common \
  docker-latest docker-latest-logrotate docker-logrotate docker-engine
```

### 2. Set up the repository
```bash
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

### 3. Install Docker Engine
```bash
sudo yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### 4. Start Docker
```bash
sudo systemctl start docker
sudo systemctl enable docker
```

---

## Uninstall

**Ubuntu / Debian / Kali:**
```bash
sudo apt-get purge -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo rm -rf /var/lib/docker /var/lib/containerd
```

**CentOS:**
```bash
sudo yum remove -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo rm -rf /var/lib/docker /var/lib/containerd
```
