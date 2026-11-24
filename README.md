# Born2beRoot — updated guide

A step-by-step guide for the 42 **Born2beRoot** project, aligned with **subject version 1.3** and **Debian 13 (trixie)**.

## What changed compared to older guides

Many guides online were written for Debian 11 or 12 and an older subject. The differences that matter:

| Topic | Older guides | Subject v1.3 |
| --- | --- | --- |
| Operating system | Debian 11 / 12, CentOS | Latest stable Debian (13) or latest stable Rocky |
| Bonus part | Advanced partitions, WordPress, extra service | No bonus chapter in the subject anymore |
| Submission | `signature.txt` only | `signature.txt` **and** `README.md` |
| Firewall | Ports 80, 8080… opened for the bonus | Only port 4242 may be open |
| Snapshots | Often recommended | No snapshot may exist when an evaluation starts |

## What the subject asks for, in short

- A VirtualBox (or UTM) virtual machine with no graphical interface.
- At least 2 encrypted partitions using LVM.
- AppArmor running at startup.
- SSH on port 4242, root login forbidden.
- UFW active at startup, only port 4242 open.
- Hostname `login42`, a user named `login` in the `sudo` and `user42` groups.
- A strong password policy.
- A strict `sudo` configuration.
- A bash script `monitoring.sh`, displayed at startup and then every 10 minutes.
- A `README.md` and a `signature.txt` at the root of the repository.

## How to read this guide

Follow the pages in the order of the table of contents. Each page ends with a **Check** section: run those commands before moving on.

In every command, replace `login` with your 42 login.

{% hint style="warning" %}
Understand each command before you type it. During the defense you will have to explain, modify and recreate parts of the setup in front of your evaluator.
{% endhint %}

## Credits

Structure inspired by the guide at [noreply.gitbook.io/born2beroot](https://noreply.gitbook.io/born2beroot). The text, commands and script were rewritten and updated.
