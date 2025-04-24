# `/etc/libvirt` — Libvirt Configuration Directory

The `/etc/libvirt` directory holds **system-wide configuration files** for the libvirt daemon (`libvirtd`) and associated virtualization drivers (like QEMU/KVM, LXC, Xen, etc.). These configs define how virtualization services behave, how domains are defined, and how networking/storage pools are managed.

---

## Key Subdirectories and Files

### 1. **`/etc/libvirt/qemu/`**
- Contains XML configs for **persistent QEMU/KVM virtual machines**.
- Files:  
  - `*.xml` → One XML file per VM.
  - `autostart/` → Symbolic links for VMs that autostart at boot.
  
```bash
/etc/libvirt/qemu/ubuntu-vm.xml
/etc/libvirt/qemu/autostart/ubuntu-vm.xml
```

### 2. **`/etc/libvirt/qemu/networks/`**
- Stores **virtual network definitions**.
- Files:
  - `default.xml` → Default NAT network.
  - `autostart/` → Symlinks for networks that should autostart.
  
```bash
/etc/libvirt/qemu/networks/default.xml
/etc/libvirt/qemu/networks/autostart/default.xml
```

### 3. **`/etc/libvirt/storage/`**
- Persistent **storage pool definitions**.
- Used by `virsh pool-*` and `virsh vol-*` commands.

### 4. **`/etc/libvirt/libvirtd.conf`**
- Main configuration file for the `libvirtd` daemon (deprecated in `libvirt >=9.0.0`, replaced by `virtproxyd`).
- Controls:
  - Listening interfaces (`unix`, `tcp`, `tls`)
  - Authentication mechanisms
  - Logging and group permissions

### 5. **`/etc/libvirt/libvirt.conf`**
- User-specific settings for libvirt clients like `virsh`.
- Affects remote connections and auth behavior (e.g., `qemu+ssh`).

---

## Autostart Mechanism

When a domain, network, or storage pool is marked to autostart, libvirt **creates a symlink** in the respective `autostart/` directory:

```bash
/etc/libvirt/qemu/autostart/vm-name.xml -> ../vm-name.xml
```

You can manage autostart via:

```bash
virsh autostart vm-name
virsh net-autostart default
```

---

## Security Contexts

If SELinux or AppArmor is enabled, libvirt uses **security labels** defined here:

- `/etc/libvirt/qemu.conf`: SELinux/AppArmor settings for QEMU/KVM
- Example: Enable dynamic labels (`dynamic_ownership = 1`)

---

## Backup and Version Control

To back up all persistent VMs, virtual networks, and storage definitions:

```bash
cp -r /etc/libvirt /backup/libvirt-$(date +%F)
```

To track changes over time:

```bash
git init /etc/libvirt
git commit -am "Initial libvirt configs"
```

---

## Summary

| Path                                | Purpose                                   |
|-------------------------------------|-------------------------------------------|
| `/etc/libvirt/qemu/*.xml`          | Persistent VM definitions                 |
| `/etc/libvirt/qemu/networks/*.xml` | Virtual network definitions               |
| `/etc/libvirt/storage/*.xml`       | Storage pool definitions                  |
| `/etc/libvirt/libvirtd.conf`       | Daemon settings (deprecated for newer)    |
| `/etc/libvirt/libvirt.conf`        | Client-side settings                      |
| `*/autostart/`                     | Symlinks for auto-started resources       |

---

Let me know if you want visuals, config examples, or comparisons with `/var/lib/libvirt` and other runtime paths.
