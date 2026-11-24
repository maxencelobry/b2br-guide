# signature.txt and snapshots

The Git repository holds only two files: `README.md` and `signature.txt`.

{% hint style="danger" %}
Putting the virtual machine in the repository is forbidden. If the signature in the repository does not match the disk on evaluation day, the grade is 0.
{% endhint %}

## Generate the signature

1. **Shut down** the VM cleanly:

   ```bash
   sudo shutdown now
   ```

2. On the host, go to the VM folder and compute the SHA-1 hash of the disk:

   | Host system | Command |
   | --- | --- |
   | Linux | `sha1sum born2beroot.vdi` |
   | macOS (VirtualBox) | `shasum born2beroot.vdi` |
   | Apple Silicon Mac (UTM) | `shasum born2beroot.utm/Images/disk-0.qcow2` |
   | Windows | `certUtil -hashfile born2beroot.vdi sha1` |

3. Copy the 40 characters of the hash into `signature.txt`:

   ```bash
   sha1sum born2beroot.vdi | cut -d ' ' -f 1 > signature.txt
   ```

4. Push `signature.txt` and `README.md` to the repository.

## The signature changes as soon as the VM starts

Starting the VM modifies the disk, and therefore its hash. Once the signature is generated, **do not start the original VM again**.

For each evaluation, work on a copy:

1. In VirtualBox, right-click the VM, **Clone**, option **Full clone**.
2. Before starting, check that the hash of the original disk still matches `signature.txt`.
3. Run the evaluation on the clone, then delete it.

## Snapshot rule

- **No snapshot** may exist when an evaluation starts.
- A dedicated snapshot may be created during the defense. It is deleted at the end.

Practise creating, restoring and deleting a snapshot before you submit the project.

## Check

```bash
sha1sum born2beroot.vdi
cat signature.txt
```

Both hashes must be identical, and the VM's snapshot list must be empty.
