# Password policy 🔑

## What the subject asks for

| Rule | Value |
| --- | --- |
| Expiration | every 30 days |
| Minimum delay between two changes | 2 days |
| Warning before expiration | 7 days |
| Minimum length | 10 characters |
| Content | one uppercase letter, one lowercase letter, one digit |
| Identical consecutive characters | 3 at most |
| User name | forbidden in the password |
| Difference with the previous password | at least 7 characters (does not apply to root) |

The root password must follow this policy too.

## 1. Password ageing: `/etc/login.defs`

```bash
sudo nano /etc/login.defs
```

Set these three values:

```
PASS_MAX_DAYS   30
PASS_MIN_DAYS   2
PASS_WARN_AGE   7
```

## 2. Apply to existing accounts: `chage`

`/etc/login.defs` only applies to accounts created **after** the change. For root and your user, which already exist:

```bash
sudo chage -M 30 -m 2 -W 7 root
sudo chage -M 30 -m 2 -W 7 login
```

{% hint style="warning" %}
This is the most common thing people forget. Without `chage`, `chage -l login` still shows `99999` days and the evaluator will see it.
{% endhint %}

## 3. Complexity: `pam_pwquality`

```bash
sudo apt install libpam-pwquality
sudo nano /etc/pam.d/common-password
```

Find the line containing `pam_pwquality.so retry=3` and complete it:

```
password  requisite  pam_pwquality.so retry=3 minlen=10 ucredit=-1 lcredit=-1 dcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root
```

| Option | Effect |
| --- | --- |
| `minlen=10` | ➤ at least 10 characters |
| `ucredit=-1` | ➤ at least one uppercase letter |
| `lcredit=-1` | ➤ at least one lowercase letter |
| `dcredit=-1` | ➤ at least one digit |
| `maxrepeat=3` | ➤ no more than 3 identical characters in a row |
| `reject_username` | ➤ rejects the user name inside the password |
| `difok=7` | ➤ 7 characters that differ from the previous password |
| `enforce_for_root` | ➤ applies these rules to root as well |

**Why `difok` does not apply to root**: when root changes a password, the old one is not asked. The module has nothing to compare against, so the 7-character rule is skipped. That is exactly the exception described in the subject.

## 4. Change every password

The subject requires it once the configuration is done:

```bash
sudo passwd login
sudo passwd root
```

## Check

```bash
sudo chage -l login
sudo chage -l root
```

Expected lines:

```
Minimum number of days between password change          : 2
Maximum number of days between password change          : 30
Number of days of warning before password expires       : 7
```

Also try a weak password:

```bash
passwd
```

A password such as `abc` must be rejected.
