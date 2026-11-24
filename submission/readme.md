# README.md

Since the current subject version, a `README.md` file is **mandatory** at the root of the repository, alongside `signature.txt`.

English is recommended. The main language of your campus is also accepted.

## Required content

1. **First line**, in italics, word for word:

   ```markdown
   *This activity has been created as part of the 42 curriculum by login.*
   ```

2. A **Description** section: the goal of the project and a short overview.
3. An **Instructions** section: how to install and run it.
4. A **Resources** section: the references you used (documentation, articles, tutorials) **and** a description of how AI was used, stating for which tasks and which parts.

## Born2beRoot-specific additions

The project description must also:

- explain your **choice of operating system** (Debian or Rocky), with the pros and cons of each;
- describe your **design choices**: partitioning, security policies, user management, installed services;
- compare:
  - Debian and Rocky Linux,
  - AppArmor and SELinux,
  - UFW and firewalld,
  - VirtualBox and UTM.

## Skeleton

```markdown
*This activity has been created as part of the 42 curriculum by login.*

# Born2beRoot

## Description

## Instructions

## Project description

### Operating system choice

### Design choices

#### Partitioning

#### Security policies

#### User management

#### Installed services

### Comparisons

#### Debian vs Rocky Linux

#### AppArmor vs SELinux

#### UFW vs firewalld

#### VirtualBox vs UTM

## Resources

### References

### AI usage
```

## Starting points for the comparisons

These are only starting points. Write them in your own words: the evaluator may ask questions about them.

| Comparison | First | Second |
| --- | --- | --- |
| Debian / Rocky | Community-driven, `.deb` packages and `apt`, easy to get started | RHEL-compatible, `.rpm` packages and `dnf`, enterprise-oriented |
| AppArmor / SELinux | Path-based rules, simple | Label-based rules, finer and more complex |
| UFW / firewalld | Short syntax, simple rules | Zones, changes applied at runtime |
| VirtualBox / UTM | x86 processors, Windows, Linux, Intel macOS | Apple Silicon Macs, built on QEMU |

## Check

- The first line is in italics and contains your login.
- The Description, Instructions and Resources sections exist.
- All four comparisons are there.
- AI usage is described.
