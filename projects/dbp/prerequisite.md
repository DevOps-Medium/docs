---
tags: []
howto: false
title: Prerequisite
description: This Project is a Practice project for DevOps Beginners.
---

# Prerequisite

This Project is a Practice project for DevOps Beginners.

You will need following things for this Project:

1. An IAM Role with AWS Administrator permissions: **_DevOps-EC2-Role_**
2. A VPC with 10.0.0.0/16 CIDR: **_DevOps-VPC_**
3. A IGW in VPC: **_DevOps-IGW_**
4. A Public Subnet in VPC with CIDR 10.0.0.0/24: **_DevOps-Subnet-01_**
5. A Key Pair for Devops EC2: **_DevOps-KP_**
6. A Security allowing all access to myIp: **_DevOps-SG_**
7. A EC2 in public Subnet with Elastic IP, IAM Role **DevOps-EC2-Role** and Security Group **DevOps-SG** on OS (Operating System) **Ubuntu 22.04**: **_DevOps-EC2_**.
8. Install following tools in DevOps-EC2:
   - [Ansible](http://localhost:3000/projects/DBP/Prerequisite#ansible)
   - [AWS CLI](http://localhost:3000/projects/DBP/Prerequisite#aws-cli)
   - [Docker](http://localhost:3000/projects/DBP/Prerequisite#docker)
   - GIT
   - [Jenkins](http://localhost:3000/projects/DBP/Prerequisite#jenkins)
   - [Terraform](http://localhost:3000/projects/DBP/Prerequisite#terraform)

Use following scripts to install the tools.

### Ansible

```bash
#!/bin/bash

set -euxo pipefail

apt update
apt upgrade -y

apt install -y software-properties-common python3 python3-pip

add-apt-repository --yes --update ppa:ansible/ansible

apt install -y ansible

ansible --version
```

### AWS CLI

```bash
#!/bin/bash

apt-get update
apt install curl unzip -y
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "/tmp/awscliv2.zip"
unzip -q /tmp/awscliv2.zip -d /tmp/
sudo /tmp/aws/install
```

### Docker

```bash
#!/bin/bash

apt-get update
apt-get upgrade -y

for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do  apt-get remove $pkg; done

# Add Docker's official GPG key:
apt-get update
apt-get install ca-certificates curl
install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
chmod a+r /etc/apt/keyrings/docker.asc


# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
   tee /etc/apt/sources.list.d/docker.list > /dev/null
apt-get update

# Installing Docker
apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-compose -y
```

### Jenkins

```bash
#!/bin/bash
apt-get update
apt-get upgrade -y
wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
apt-get update
apt-get install fontconfig -y
apt-get install openjdk-17-jre -y
apt-get install jenkins -y
systemctl enable jenkins
systemctl start jenkins
```

### Terraform

```bash
#!/bin/bash

apt update
apt upgrade -y

apt install -y gnupg software-properties-common

wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hashicorp.list

apt update

apt install terraform -y
```
