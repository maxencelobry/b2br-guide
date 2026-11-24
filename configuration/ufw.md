# UFW 🔥🧱 firewall

The subject asks for UFW, **active at startup**, with **only port 4242 open**.

## Install and enable

```bash
sudo apt install ufw
sudo ufw allow 4242
sudo ufw enable
```

Allow port 4242 **before** `ufw enable`: if you are connected over SSH, you keep your session.

`ufw enable` turns the firewall on right away and at every boot.

## Manage rules

| Action | Command |
| --- | --- |
| Show numbered rules | `sudo ufw status numbered` |
| Open a port | `sudo ufw allow 8080` |
| Delete a rule by number | `sudo ufw delete 2` |
| Delete a rule by port | `sudo ufw delete allow 8080` |

During the defense you will be asked to open port 8080 and then delete that rule. After a deletion the numbers shift: run `sudo ufw status numbered` again before deleting the next one.

{% hint style="warning" %}
Do not leave any other port open. Older guides open 80 or 8080 for a WordPress bonus: with the current subject that breaks the "only port 4242 open" rule.
{% endhint %}

## Check

```bash
sudo ufw status
systemctl is-enabled ufw
```

Expected result:

```
Status: active

To                         Action      From
--                         ------      ----
4242                       ALLOW       Anywhere
4242 (v6)                  ALLOW       Anywhere (v6)
```

Only the `4242` rules must appear, and `is-enabled` must answer `enabled`.
