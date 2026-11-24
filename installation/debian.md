# Installing Debian 13

Start the VM. In the installer menu, choose **Install** (text mode), not **Graphical install**.

<figure><img src="../.gitbook/assets/01-menu-install.png" alt="Debian installer menu with Install selected"><figcaption></figcaption></figure>

{% hint style="danger" %}
The subject forbids any graphical server (X.org, Wayland or equivalent). Installing one means a grade of 0.
{% endhint %}

## Language, location, keyboard

1. **Language**: <mark style="color:green;">English</mark> (error messages are easier to search for).

<figure><img src="../.gitbook/assets/02-language.png" alt="Language selection"><figcaption></figcaption></figure>

2. **Location**: your country. If it is not in the short list, choose `other`.

<figure><img src="../.gitbook/assets/03-location.png" alt="Location selection"><figcaption></figcaption></figure>

3. **Keymap**: the layout of your physical keyboard.

<figure><img src="../.gitbook/assets/04-keymap.png" alt="Keymap selection"><figcaption></figcaption></figure>

## Network

1. **Hostname**: your login followed by `42`, for example `wil42`. This is a subject requirement.

<figure><img src="../.gitbook/assets/05-hostname.png" alt="Hostname set to login42"><figcaption></figcaption></figure>

2. **Domain name**: leave it empty.

<figure><img src="../.gitbook/assets/06-domain.png" alt="Empty domain name"><figcaption></figcaption></figure>

## Users

1. **Root password**: pick one that already follows the subject's policy (at least 10 characters, one uppercase letter, one lowercase letter, one digit, no more than 3 identical characters in a row). The installer asks for it twice.

<figure><img src="../.gitbook/assets/07-root-password.png" alt="Root password prompt"><figcaption></figcaption></figure>

{% hint style="info" %}
Setting a root password here means `sudo` is **not** installed. That is intended: the subject asks you to install and configure it yourself.
{% endhint %}

2. **Full name**: your login.

<figure><img src="../.gitbook/assets/08-fullname.png" alt="Full name of the new user"><figcaption></figcaption></figure>

3. **Username**: your login.

<figure><img src="../.gitbook/assets/09-username.png" alt="Username of the new user"><figcaption></figcaption></figure>

4. **Password**: same rule as for root, asked twice.

<figure><img src="../.gitbook/assets/10-user-password.png" alt="User password prompt"><figcaption></figcaption></figure>

## Clock

Select your time zone.

<figure><img src="../.gitbook/assets/11-clock.png" alt="Time zone selection"><figcaption></figcaption></figure>

## Partitioning

This step has its own page: [Encrypted partitions and LVM](partitions.md). Do it, then come back here.

## Package manager

1. **Scan extra installation media**: <mark style="color:green;">No</mark>.

<figure><img src="../.gitbook/assets/22-extra-media.png" alt="Scan extra installation media prompt"><figcaption></figcaption></figure>

2. **Mirror country**: your country.

<figure><img src="../.gitbook/assets/23-mirror-country.png" alt="Mirror country selection"><figcaption></figcaption></figure>

3. **Mirror**: <mark style="color:green;">deb.debian.org</mark>.

<figure><img src="../.gitbook/assets/24-mirror.png" alt="Mirror selection"><figcaption></figcaption></figure>

4. **HTTP proxy**: leave it empty.

<figure><img src="../.gitbook/assets/25-proxy.png" alt="Empty HTTP proxy"><figcaption></figcaption></figure>

5. **Popularity contest**: <mark style="color:green;">No</mark>.

<figure><img src="../.gitbook/assets/26-popcon.png" alt="Popularity contest prompt"><figcaption></figcaption></figure>

## Software selection

Untick **everything** with the space bar, including `Debian desktop environment`, `GNOME` and `standard system utilities`, then **Continue**.

<figure><img src="../.gitbook/assets/27-tasksel.png" alt="Software selection with everything unticked"><figcaption></figcaption></figure>

SSH is installed by hand later so that you understand what you are doing.

## GRUB

1. **Install the GRUB boot loader to your primary drive**: <mark style="color:green;">Yes</mark>.

<figure><img src="../.gitbook/assets/28-grub.png" alt="GRUB install prompt"><figcaption></figcaption></figure>

2. Device: <mark style="color:green;">/dev/sda</mark>.

<figure><img src="../.gitbook/assets/29-grub-device.png" alt="GRUB device selection"><figcaption></figcaption></figure>

3. **Continue** to reboot.

<figure><img src="../.gitbook/assets/30-finish.png" alt="Installation complete"><figcaption></figcaption></figure>

## Check

After the reboot:

1. The VM asks for the disk **encryption passphrase**.

<figure><img src="../.gitbook/assets/31-unlock.png" alt="Prompt to unlock sda5_crypt"><figcaption></figcaption></figure>

2. It then shows a text login prompt, with no graphical interface. Log in with your login.

<figure><img src="../.gitbook/assets/32-login-prompt.png" alt="Text login prompt"><figcaption></figcaption></figure>
