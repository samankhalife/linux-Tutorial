# `guestumount` — Virtual Disk Image Unmounting Tool

`guestumount` is a command-line utility from the **libguestfs** toolkit. It allows you to unmount filesystems from within virtual machine (VM) disk images without needing to boot the VM. This is particularly useful for VM image maintenance, automation, and safe file system handling in virtualized environments.

---

## Key Features

- **Unmount Filesystems in Disk Images**: Cleanly unmount individual or all filesystems in VM disk images.
- **Supports Multiple Disk Formats**: Compatible with `qcow2`, `raw`, `vmdk`, `vdi`, and more.
- **No VM Boot Required**: Manage filesystems offline, reducing VM downtime and risk.
- **Essential for Disk Image Cleanup**: Ensures images are in a consistent state for backup, deployment, or modification.

---

## Basic Syntax

```bash
guestumount [options] <mount_point>
```

- `<mount_point>`: Directory where the image filesystem was mounted (e.g., `/mnt`).
- Requires that the image was previously mounted using `guestmount`.

---

## Common Options

- `-h`, `--help`: Show help and usage information.
- `-v`, `--verbose`: Output more detailed logs of operations.
- `-a`, `--all`: Unmount all currently mounted filesystems.
- `-f`, `--force`: Force unmount even if the filesystem is busy or in a problematic state.
- `--list`: Show all mounted filesystems from libguestfs context.

---

## Example Use Cases

### Unmount a Specific Filesystem

Unmount a previously mounted filesystem from a disk image:

```bash
guestumount /mnt
```

This command unmounts the filesystem mounted at `/mnt`, assuming it was mounted using `guestmount`.

---

### Unmount All Filesystems

To cleanly unmount all libguestfs-mounted filesystems:

```bash
guestumount --all
```

Useful during cleanup scripts or before shutting down a libguestfs session.

---

### Force Unmount

To unmount a filesystem that may be in an inconsistent state:

```bash
guestumount --force /mnt
```

This is helpful if standard unmounting fails due to a locked or partially modified mount.

---

### List Currently Mounted Filesystems

To display what libguestfs sees as mounted:

```bash
guestumount --list
```

This outputs all current libguestfs mounts, helping track what needs to be unmounted.

---

## Example Output

```bash
Unmounting /mnt from disk image context...
```

If running `--list`:

```bash
/dev/sda1  /mnt
/dev/sdb1  /data
```

---

## Use Case Scenarios

- **VM Image Maintenance**: Allows safe unmounting of modified filesystems before packaging or deploying VM images.
- **Automated Cleanup**: Integrates into scripts that perform actions on disk images (e.g., testing, CI/CD pipelines).
- **Forensic Analysis**: Enables unmounting after inspecting or extracting data from compromised or test VM disk images.
- **Backup Preparation**: Ensures all file operations are finalized before archiving or converting the disk image.

---

## Conclusion

`guestumount` is a reliable and necessary utility for managing disk image mounts in virtualized environments. It ensures that virtual disk changes are finalized cleanly, supports automation workflows, and helps maintain disk image integrity without requiring the virtual machine to run.
