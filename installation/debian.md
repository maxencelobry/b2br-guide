# Installing Debian 13

Start the VM. In the installer menu, choose **Install** (text mode), not **Graphical install**.

{% hint style="danger" %}
The subject forbids any graphical server (X.org, Wayland or equivalent). Installing one means a grade of 0.
{% endhint %}

## Language, location, keyboard

1. **Language**: English (error messages are easier to search for).
2. **Location**: your country.
3. **Locale**: `en_US.UTF-8`.
4. **Keymap**: the layout of your physical keyboard.

## Network

1. **Hostname**: your login followed by `42`, for example `wil42`. This is a subject requirement.
2. **Domain name**: leave it empty.

## Users

1. **Root password**: pick one that already follows the subject's policy (at least 10 characters, one uppercase letter, one lowercase letter, one digit, no more than 3 identical characters in a row).
2. **Full name** and **Username**: your login.
3. **Password**: same rule as for root.

{% hint style="info" %}
Setting a root password during installation means `sudo` is **not** installed. That is intended: the subject asks you to install and configure it yourself.
{% endhint %}

## Partitioning

This step has its own page: [Encrypted partitions and LVM](partitions.md). Do it, then come back here.

## Package manager

1. **Scan extra installation media**: No.
2. **Mirror country**: your country, then `deb.debian.org`.
3. **HTTP proxy**: leave it empty.
4. **Popularity contest**: No.

## Software selection

Untick **everything**, including `Debian desktop environment`, `GNOME` and `SSH server`. Use the space bar to untick, then **Continue**.

SSH is installed by hand later so that you understand what you are doing.

## GRUB

1. **Install the GRUB boot loader to your primary drive**: Yes.
2. Device: `/dev/sda`.

The installation finishes and the VM reboots.

## Check

After the reboot:

1. The VM asks for the disk **encryption passphrase**.
2. It then shows a text login prompt, with no graphical interface.
3. You can log in with your login.
