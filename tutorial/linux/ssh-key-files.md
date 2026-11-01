---
tags: []
howto: false
title: Decoding SSH Key Files
description: A breakdown of public/private SSH Key Files (pem and ppk) used for authentication.
---

# Decoding SSH Key Files

SSH (Secure Shell) is a protocol used to securely log into remote systems. Instead of using a password, you can authenticate using **SSH key pairs**. This method is more secure and commonly used for managing remote servers, especially in cloud environments like AWS.

## 🔐 What are SSH Keys?

SSH key-based authentication uses a **pair of cryptographic keys**:

- **Private Key** – kept secret by the user.
- **Public Key** – placed on the remote system you want to access.

## 📁 Common SSH Key File Formats

### `.pem` (Privacy Enhanced Mail)

- **Default format for AWS EC2 key pairs**.
- PEM files are used by OpenSSH (Linux/macOS) for SSH authentication.
- Typically used directly with the `ssh` command.

### `.ppk` (PuTTY Private Key)

- A format used by **PuTTY**, a popular SSH client on Windows.
- You can convert `.pem` to `.ppk` using **PuTTYgen**.

## 🔧 Using SSH Keys in Linux

### 1. Connect Using a `.pem` File

If you have a `.pem` file (e.g., from AWS EC2):

```bash
chmod 400 my-key.pem
ssh -i my-key.pem username@remote-host
```
