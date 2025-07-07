---
date: '2025-07-07T21:02:34+03:00'
draft: false
title: 'Fresh VPS Hardening'
---

## Assumptions
- Ubuntu LTS distribution
- SSH connection already established
- Root SSH keys already set up

## Create a non-root user with sudo privileges
```bash
adduser newusername
usermod -aG sudo newusername
```

## Set up SSH keys for new user
```bash
mkdir -p /home/newusername/.ssh
cp /root/.ssh/authorized_keys /home/newusername/.ssh/
chown -R newusername:newusername /home/newusername/.ssh
chmod 700 /home/newusername/.ssh
chmod 600 /home/newusername/.ssh/authorized_keys
```

## Harden SSH configuration
```bash
nano /etc/ssh/sshd_config
```
Add/modify these lines:
```
PermitRootLogin no
PasswordAuthentication no
PermitEmptyPasswords no
Port 58923  # Change default SSH port
AllowUsers newusername
```
Restart SSH:
```bash
systemctl disable --now ssh.socket
systemctl enable --now ssh.service
```

## Update system
```bash
apt update && apt upgrade -y
```

## Configure UFW firewall
```bash
ufw default deny incoming
ufw default allow outgoing
ufw allow 58923/tcp  # SSH port you configured
ufw allow 80/tcp    # HTTP (if needed)
ufw allow 443/tcp   # HTTPS (if needed)
ufw enable
```

## Install fail2ban
```bash
apt install fail2ban
cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
nano /etc/fail2ban/jail.local
```
Configure fail2ban:

**Important note:** There is already an sshd section enabled in the config. Do not enable the commented-out sshd section in the config.
```
[sshd]
enabled = true
port    = 58923
bantime = 3600
findtime = 600
maxretry = 5
```
Restart fail2ban:
```bash
systemctl enable fail2ban
systemctl restart fail2ban
```

## Secure shared memory
Add to `/etc/fstab`:
```
tmpfs /run/shm tmpfs defaults,noexec,nosuid 0 0
```

## Enable automatic security updates
```bash
apt install unattended-upgrades
dpkg-reconfigure -plow unattended-upgrades
```

## Configure system-wide security settings
Edit `/etc/sysctl.conf`:
```
# Protect against SYN flood
net.ipv4.tcp_syncookies = 1

# Disable IP forwarding
net.ipv4.ip_forward = 0

# Disable IP source routing
net.ipv4.conf.all.accept_source_route = 0
net.ipv4.conf.default.accept_source_route = 0

# Enable reverse path filtering
net.ipv4.conf.all.rp_filter = 1
net.ipv4.conf.default.rp_filter = 1

# Disable ICMP redirect acceptance
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.default.accept_redirects = 0
```
Apply changes:
```bash
sysctl -p
```

## Remove unnecessary services
```bash
apt autoremove --purge
```

## Reboot

Not necessary but recommended for all changes to take effect:
```bash
reboot
```