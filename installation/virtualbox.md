# Creating the virtual machine

## Download the image

The subject requires the **latest stable version** of Debian. Get the `netinst` image for `amd64` from [debian.org/distrib/netinst](https://www.debian.org/distrib/netinst).

The file is named `debian-13.x.0-amd64-netinst.iso`. The `testing` and `unstable` releases are forbidden.

## Where to store the VM

The virtual disk takes several gigabytes. On 42 workstations the home quota is limited: put the VM folder in `sgoinfre` (or `goinfre`), not in your home directory.

## Create the VM in VirtualBox

1. **New**.
2. **Name**: anything you like, for example `born2beroot`.
3. **Folder**: your folder in `sgoinfre`.
4. **ISO Image**: leave it empty for now. If you set it here, tick **Skip Unattended Installation**, otherwise VirtualBox installs Debian by itself with its own settings.
5. **Type**: Linux, **Version**: Debian (64-bit).
6. **Memory**: 1024 MB is enough, 2048 MB is more comfortable.
7. **Processors**: 1.
8. **Hard disk**: create a virtual hard disk, **VDI** format, dynamically allocated, **12 GB**.

{% hint style="info" %}
The subject asks you to pick sensible partition sizes without wasting space. A minimal Debian server uses about 1 GB, but the guided encrypted LVM scheme with a separate `/home` needs at least <mark style="color:green;">9 GB</mark>: 12 GB is a safe choice.
{% endhint %}

## Attach the ISO

1. Select the VM, then **Settings > Storage**.
2. Click the empty optical drive (**Empty**).
3. Disc icon on the right, **Choose a disk file**, then select the Debian ISO.

## Port forwarding for SSH

The VM uses **NAT** networking. To reach it over SSH from the host, a port must be forwarded.

1. **Settings > Network > Adapter 1 > Advanced > Port Forwarding**.
2. Add a rule:

| Name | Protocol | Host Port | Guest Port |
| --- | --- | --- | --- |
| ssh | TCP | 4242 | 4242 |

If port 4242 is already taken on the host, use another host port (for example 4243). The **Guest Port** stays 4242: that is the one the subject requires inside the VM.

## Check

- The VM shows up in VirtualBox with a 12 GB VDI disk.
- The Debian ISO is attached to the optical drive.
- No snapshot exists.
