# SSH

The subject asks for an SSH service on **port 4242**, with no way to connect as **root**.

## Install

```bash
sudo apt install openssh-server
```

## Configure

Edit the **server** configuration file:

```bash
sudo nano /etc/ssh/sshd_config
```

Change these two lines (remove the leading `#`):

```
Port 4242
PermitRootLogin no
```

{% hint style="info" %}
Do not mix up `sshd_config` (server) and `ssh_config` (client). Only `sshd_config` has to change. Setting the port in `ssh_config` does nothing for this project.
{% endhint %}

Restart the service:

```bash
sudo systemctl restart ssh
```

## Connect from the host

With the port forwarding rule created in VirtualBox (host 4242 to guest 4242), from a terminal on your host machine:

```bash
ssh login@localhost -p 4242
```

If you picked another host port, use that one after `-p`.

## Check

Inside the VM:

```bash
sudo systemctl status ssh
sudo ss -tlnp | grep sshd
```

The service must be `active (running)` and listen on port `4242`.

From the host, root login must be refused:

```bash
ssh root@localhost -p 4242
```

Expected result after typing the password: `Permission denied`.
