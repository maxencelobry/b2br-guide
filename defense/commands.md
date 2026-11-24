# Evaluation commands

A typical evaluation run. Practise doing all of it without the guide.

## Before starting

```bash
sha1sum born2beroot.vdi
```

The hash must match `signature.txt`. No snapshot may exist.

## System

| Check | Command |
| --- | --- |
| No graphical interface | `ls /usr/bin/*session` |
| Installed system | `cat /etc/os-release` |
| Kernel | `uname -a` |
| AppArmor running | `sudo aa-status` |
| Partitions | `lsblk` |

`ls /usr/bin/*session` must not list any graphical session manager (`gnome-session`, `xfce4-session`…). `dbus-run-session` may appear, it is not a graphical interface.

## Services

| Check | Command |
| --- | --- |
| UFW active | `sudo ufw status` |
| UFW at startup | `systemctl is-enabled ufw` |
| SSH active | `sudo systemctl status ssh` |
| SSH port | `sudo ss -tlnp \| grep sshd` |
| Cron active | `sudo systemctl status cron` |

## User and groups

```bash
getent group sudo user42
sudo chage -l login
```

### Create a user

```bash
sudo adduser newuser
sudo chage -l newuser
```

The chosen password must follow the policy. `chage -l` must show 2, 30 and 7 days.

### Create a group and add the user to it

```bash
sudo addgroup evaluating
sudo adduser newuser evaluating
getent group evaluating
```

## Hostname

```bash
hostname
```

Expected result: `login42`.

### Change the hostname

```bash
sudo hostnamectl set-hostname newname42
sudo nano /etc/hosts
sudo reboot
```

In `/etc/hosts`, replace the old name with the new one on the `127.0.1.1` line. After the reboot, check with `hostname`, then restore the original name the same way.

## sudo

```bash
sudo cat /etc/sudoers.d/sudo_config
sudo ls /var/log/sudo
sudo cat /var/log/sudo/sudo.log
```

Run a command with sudo, then show that `sudo.log` has one more line.

Add the new user to the sudo group:

```bash
sudo adduser newuser sudo
```

## UFW

```bash
sudo ufw status numbered
sudo ufw allow 8080
sudo ufw status numbered
sudo ufw delete allow 8080
sudo ufw status numbered
```

At the end, only the `4242` rules must remain.

## SSH

From the host machine:

```bash
ssh newuser@localhost -p 4242
ssh root@localhost -p 4242
```

The first connection must succeed, the second must be refused.

## Script and cron

```bash
sudo crontab -u root -l
sudo crontab -u root -e
```

- Change the interval from `*/10` to `*/1` and show that the message arrives every minute.
- Stop the script without modifying it:

  ```bash
  sudo systemctl disable --now cron
  sudo reboot
  ```

- After the reboot, show that the script is still in the same place, unchanged, and no longer displayed:

  ```bash
  ls -l /usr/local/bin/monitoring.sh
  systemctl is-enabled cron
  ```

- Re-enable cron:

  ```bash
  sudo systemctl enable --now cron
  ```
