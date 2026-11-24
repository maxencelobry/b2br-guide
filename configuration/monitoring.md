# monitoring.sh script

The subject asks for a **bash** script named `monitoring.sh`. It is displayed on every terminal at server startup, then every 10 minutes. **No error may be displayed.**

## Information to display

1. Operating system architecture and kernel version.
2. Number of physical processors.
3. Number of virtual processors.
4. RAM in use and its percentage.
5. Disk space in use and its percentage.
6. CPU load as a percentage.
7. Date and time of the last boot.
8. Whether LVM is active.
9. Number of active connections.
10. Number of logged-in users.
11. IPv4 address and MAC address.
12. Number of commands run with sudo.

## Create the script

```bash
sudo nano /usr/local/bin/monitoring.sh
```

```bash
#!/bin/bash

arch=$(uname -a)
pcpu=$(grep "physical id" /proc/cpuinfo | sort -u | wc -l)
vcpu=$(grep -c "^processor" /proc/cpuinfo)
ram=$(free --mega | awk '$1 == "Mem:" {printf "%d/%dMB (%.2f%%)", $3, $2, $3 / $2 * 100}')
disk=$(df -m -x tmpfs -x devtmpfs --total | awk '$1 == "total" {printf "%d/%dMB (%s)", $3, $2, $5}')
cpu=$(vmstat 1 2 | tail -1 | awk '{printf "%.1f%%", 100 - $15}')
boot=$(uptime -s | cut -c 1-16)
lvm=$(if lsblk | grep -q "lvm"; then echo yes; else echo no; fi)
tcp=$(ss -Ht state established | wc -l)
users=$(who | wc -l)
ip=$(hostname -I | awk '{print $1}')
mac=$(ip link show | awk '/link\/ether/ {print $2; exit}')
sudo=$(journalctl _COMM=sudo 2>/dev/null | grep -c "COMMAND")

wall "	#Architecture: $arch
	#Physical CPU: $pcpu
	#vCPU: $vcpu
	#Memory Usage: $ram
	#Disk Usage: $disk
	#CPU load: $cpu
	#Last boot: $boot
	#LVM use: $lvm
	#TCP Connections: $tcp ESTABLISHED
	#User log: $users
	#Network: IP $ip ($mac)
	#Sudo: $sudo cmd"
```

Make it executable:

```bash
sudo chmod +x /usr/local/bin/monitoring.sh
```

## Line by line

| Variable | Command | What it does |
| --- | --- | --- |
| `arch` | `uname -a` | Prints the kernel, its version and the architecture. |
| `pcpu` | `grep "physical id" /proc/cpuinfo \| sort -u \| wc -l` | Each physical processor has its own `physical id`. `sort -u` removes duplicates, `wc -l` counts. |
| `vcpu` | `grep -c "^processor" /proc/cpuinfo` | Counts the `processor` lines, one per logical core. |
| `ram` | `free --mega` + `awk` | On the `Mem:` line, `$2` is the total and `$3` is the used amount. `awk` computes the percentage. |
| `disk` | `df -m --total` + `awk` | `--total` adds a sum line. `-x tmpfs -x devtmpfs` leaves out in-memory filesystems. |
| `cpu` | `vmstat 1 2` + `awk` | Takes two samples one second apart. Column 15 of the last line is the idle percentage: `100 - idle` gives the load. |
| `boot` | `uptime -s` | Boot date and time. `cut` drops the seconds. |
| `lvm` | `lsblk \| grep -q "lvm"` | Answers `yes` if at least one device has type `lvm`. |
| `tcp` | `ss -Ht state established` | Lists established TCP connections, without a header. `wc -l` counts. |
| `users` | `who \| wc -l` | One line per open session. |
| `ip` | `hostname -I` | The machine's IP addresses. `awk` keeps the first one. |
| `mac` | `ip link show` + `awk` | Keeps the address from the first `link/ether` line. |
| `sudo` | `journalctl _COMM=sudo \| grep -c "COMMAND"` | Each sudo command writes a `COMMAND` line to the journal. |

`wall` sends the message to every open terminal.

{% hint style="info" %}
Why `vmstat 1 2` and not plain `vmstat`: the first line of `vmstat` is an average since boot. Only the second sample reflects the current load.
{% endhint %}

{% hint style="info" %}
On UTM (ARM Macs), `/proc/cpuinfo` has no `physical id` line: the script prints `0`. Replace the command with `lscpu | awk '/^Socket\(s\)/ {print $2}'`.
{% endhint %}

## Check

```bash
sudo bash /usr/local/bin/monitoring.sh
```

The message must show up on your terminal, with all 12 lines filled in and **no error message**. Compare the values with `free --mega`, `df -m`, `lsblk` and `hostname -I`.
