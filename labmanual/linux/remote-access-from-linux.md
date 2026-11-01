---
tags: []
howto: false
title: Remote Access from Linux
description: Step-by-step guide to remotely access linux machine from linux using OpenSSH.
---

# Remote Access from Linux

OpenSSH (Open Secure Shell) is a widely used tool that allows secure remote login from one computer to another over a network. In this guide, you will learn how to access a remote Linux machine from a local Linux machine using OpenSSH.

## Prerequisites

- You must have two Linux machines (local and remote).
- The remote machine must have SSH server installed and running.
- You must know the remote machine’s IP address and the credentials to log in.

---

## Step 1: Verify OpenSSH Installation

### On the **Local Machine** (Client)

Check if the SSH client is installed:

```bash
ssh -V
```

If not installed, install it using:

- For Ubuntu/Debian

```bash
sudo apt update
sudo apt install openssh-client
```

- For CentOS/Fedora/RHEL (Red Hat Enterprise Linus)

```bash
sudo yum install openssh-clients
```
