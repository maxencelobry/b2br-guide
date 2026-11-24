# Theory questions

Short answers to the most common questions. Rephrase them in your own words.

## Virtual machine

**How does a virtual machine work?**
A program called a hypervisor (here VirtualBox) simulates a full computer: processor, memory, disk, network card. A guest operating system is installed on it as on a real machine, isolated from the host system.

**What is it for?**
Testing a system without touching your own machine, isolating services, running several systems on one computer, rolling back easily.

## Operating system

**Why Debian?**
Stable, well documented, simple to administer, and recommended by the subject for beginners.

**Difference between Debian and Rocky?**
Debian is community-driven and uses `.deb` packages with `apt`. Rocky is a rebuild of RHEL, enterprise-oriented, with `.rpm` packages and `dnf`. Rocky uses SELinux and firewalld, Debian uses AppArmor and UFW.

**Difference between `apt` and `aptitude`?**
Both install packages. `apt` is the standard command-line tool. `aptitude` is higher level: it has a text-mode interface and offers several solutions when dependencies conflict.

**What is AppArmor?**
See the [AppArmor](../configuration/apparmor.md) page.

## Disk

**What is LVM?**
A logical volume manager. It adds a layer between disks and filesystems, which lets you resize or add volumes without repartitioning.

**Why encrypt?**
If someone gets hold of the disk file, they cannot read anything without the passphrase.

## Services

**What is SSH?**
A protocol for opening an encrypted remote session. Forbidding root login forces people to connect with a personal account and then use sudo, which leaves a trace.

**What is UFW?**
A simple front end for configuring the kernel firewall. It blocks incoming connections by default and only allows the declared ports.

**What is sudo?**
A program that lets an authorized user run a command with another user's rights, usually root, while logging the action.

**Why a password policy?**
It makes passwords harder to guess and limits how long a stolen password stays usable. Downside: rules that are too strict push users to write their passwords down.

**What is cron?**
A service that runs commands at scheduled times. Each user has a task table, edited with `crontab -e`.

## Script

You must be able to explain every line of `monitoring.sh`. The table on the [monitoring.sh script](../configuration/monitoring.md) page details each command.
