---
title: Network Configuration
description: install network-manager on debain
published: true
date: 2025-07-30T11:31:38.211Z
tags: network, debian, linux
editor: markdown
dateCreated: 2025-07-30T00:12:06.543Z
---

## 1\. Back up your current /etc/network/interfaces file

```plaintext
cp /etc/network/interfaces /etc/network/interfaces.bak
```

## 2\. Clear the main network configuration

```plaintext
cat << "EOF" > /etc/network/interfaces
auto lo
iface lo inet loopback
EOF
```

## 3\. Disable cloud-init's Network Management (optional)

```plaintext
mkdir -p /etc/cloud/cloud.cfg.d/
echo "network: {config: disabled}" | tee /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg
```

## 4\. Install NetworkManager and nmtui

```plaintext
apt update && apt install network-manager -y
```

## 5\. Enable and Start NetworkManager

```plaintext
systemctl start NetworkManager
systemctl enable NetworkManager
systemctl status NetworkManager
```

## 6\. Disable ifupdown

> Executing this command may disconnect your internet. If you're using a VPS, ensure you have VNC access or another way to reconnect before proceeding, as you might lose access to your server. Double-check to avoid getting locked out!

```plaintext
systemctl stop networking
systemctl disable networking
```

## 7\. Remove ifupdown and Clean Up (optional)

```plaintext
apt purge ifupdown -y
```

## 8\. Configure Network with nmtui

```plaintext
nmtui
```

![](/nmtui.png)