---
tags: []
howto: false
title: Git Login via SSH
description: Step-by-step guide to logging into Git using SSH.
---

# Git Login via SSH

Follow these steps to authenticate Git using SSH.

## 1. Check for Existing SSH Keys

Check if an SSH key already exists:

```bash
ls -al ~/.ssh
```

If files like `id_rsa` and `id_rsa.pub` are present, you already have a key.

## 2. Generate a New SSH Key (If Needed)

Generate a new SSH key:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Press **Enter** to save it in the default location and set an optional passphrase.

## 3. Start SSH Agent and Add Your Key

Ensure the SSH agent is running:

```bash
eval "$(ssh-agent -s)"
```

Add your key:

```bash
ssh-add ~/.ssh/id_rsa
```

## 4. Copy SSH Key to Git Provider

Copy the public key:

```bash
cat ~/.ssh/id_rsa.pub
```

Go to **GitHub/GitLab/Bitbucket** → **SSH and GPG keys** → **New SSH Key**, then paste the copied key.

## 5. Test SSH Connection

Test your connection:

### GitHub:

```bash
ssh -T git@github.com
```

### GitLab:

```bash
ssh -T git@gitlab.com
```

### Bitbucket:

```bash
ssh -T git@bitbucket.org
```

A successful connection returns a message like:

```
Hi <username>! You've successfully authenticated, but GitHub does not provide shell access.
```

## 6. Configure Git User Information

Set your Git username and email:

```bash
git config --global user.name "Your Name"
```

```bash
git config --global user.email "your_email@example.com"
```

## 7. Clone a Repository Using SSH

If cloning a new repository, use:

```bash
git clone git@github.com:your-username/your-repo.git
```

After completing these steps, you can use Git via SSH without entering your password every time. 🚀
