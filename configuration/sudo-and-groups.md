# First boot, sudo and groups

## Become root

Log in with your login, then:

```bash
su -
```

{% hint style="warning" %}
Use `su -` with the dash. Without it, `PATH` does not contain `/usr/sbin` and commands such as `adduser` or `ufw` are not found.
{% endhint %}

## Install sudo

```bash
apt update
apt install sudo
```

## Add your user to the groups

The subject requires your user to belong to the `sudo` and `user42` groups.

```bash
addgroup user42
adduser login sudo
adduser login user42
```

New groups only apply at the next login. Log out completely and log back in:

```bash
exit
exit
```

## Useful commands for the defense

The evaluator will ask you to create a user and add it to a group.

| Action | Command |
| --- | --- |
| Create a user | `sudo adduser name` |
| Create a group | `sudo addgroup group` |
| Add a user to a group | `sudo adduser name group` |
| List a user's groups | `groups name` |
| List a group's members | `getent group group` |
| Delete a user | `sudo deluser name` |

## Check

```bash
sudo whoami
getent group sudo user42
```

`sudo whoami` must print `root`. The second command must list your login in both groups.
