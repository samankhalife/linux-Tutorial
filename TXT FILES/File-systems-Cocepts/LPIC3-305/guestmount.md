`guestmount` is a utility from the `libguestfs` suite that allows you to mount a virtual machine disk image (or any supported guest filesystem) on your host system without booting the virtual machine.

---

**Purpose**  
- Access and manipulate files within VM disk images directly from the host.
- Useful for inspection, recovery, or injecting/removing files.

---

**Common Use Cases**  
- Debugging or viewing guest log/config files.  
- Copying files into or out of a VM disk image.  
- Performing forensics on a VM image.  
- Rescuing files from an unbootable image.  
- Modifying or patching guest environments.

---

**Basic Syntax**
```bash
guestmount -a <disk.img> -m <mount_point> <host_directory>
```

---

**Example:**
Mount `/dev/sda1` from `disk.qcow2` image in read-only mode to `/mnt/vm`:
```bash
guestmount -a disk.qcow2 -m /dev/sda1 --ro /mnt/vm
```

Use `-i` for automatic partition detection:
```bash
guestmount -a disk.qcow2 -i --ro /mnt/vm
```

---

**Options**
| Option     | Description                                 |
|------------|---------------------------------------------|
| `-a`       | Specify disk image                          |
| `-i`       | Auto-detect guest OS and partitions         |
| `-m`       | Specify guest partition to mount            |
| `--ro`     | Mount as read-only                          |
| `--rw`     | Mount with read/write access (use cautiously) |
| `--trace`  | Enable backend call debugging               |

---

**Filesystem Support**
- Raw, qcow2, vmdk, vdi, img
- Supports partitioned filesystems, LVM, and more.

---

**Unmounting**
Always unmount with:
```bash
guestunmount /mnt/vm
```

---

**Security Notes**
- Use `--ro` to avoid accidental changes.
- `--rw` may require root and can risk image corruption.
- Do not expose guest filesystems to untrusted scripts or users.
