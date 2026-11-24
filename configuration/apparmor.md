# AppArmor

The subject requires **AppArmor to be running at startup** on Debian. It is installed and enabled by default: there is nothing to configure, but you must check it and be able to explain it.

## Check

```bash
sudo aa-status
systemctl is-enabled apparmor
```

`aa-status` must start with `apparmor module is loaded.` and `is-enabled` must answer `enabled`.

If AppArmor is missing:

```bash
sudo apt install apparmor
sudo systemctl enable --now apparmor
```

## What you must be able to explain

AppArmor is a **mandatory access control** (MAC) system. It limits what each program is allowed to do, even when that program runs as root.

- Each protected program has a **profile** listing the files, capabilities and network access it may use.
- A profile is in **enforce** mode (violations are blocked) or **complain** mode (violations are only logged).
- Profiles live in `/etc/apparmor.d/`.

## AppArmor and SELinux

| | AppArmor | SELinux |
| --- | --- | --- |
| Distribution | Debian, Ubuntu | Rocky, RHEL, Fedora |
| Principle | rules based on file **paths** | rules based on **labels** attached to every file and process |
| Learning curve | simple | more complex |
| Granularity | enough for most cases | very fine |

This comparison is also required in the `README.md` you submit.
