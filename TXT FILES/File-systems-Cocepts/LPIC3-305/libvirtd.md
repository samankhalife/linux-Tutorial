# `libvirtd` — Libvirt Daemon (Legacy Central Virtualization Daemon)

## Overview

`libvirtd` is the **system daemon** for **libvirt**, responsible for managing virtualization hosts and hypervisors (e.g., QEMU/KVM, Xen, LXC). It exposes a **high-level API and remote protocol** to control and automate virtual machines, networks, storage, and more.

**Deprecated**: As of **libvirt 9.0 (2023)**, `libvirtd` is deprecated and has been split into modular daemons like:
- `virtqemud`
- `virtlogd`
- `virtproxyd`
- `virtnetworkd`, etc.

But it’s still widely used in existing Linux distributions.

---

## Responsibilities of `libvirtd`

| Feature                    | Description                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| Hypervisor Integration     | Interacts with QEMU, KVM, LXC, Xen, etc. via driver plugins.               |
| VM Lifecycle Management    | Start, stop, pause, resume, reboot, and destroy virtual machines.          |
| Storage Management         | Create/delete volumes and pools, attach storage.                           |
| Network Management         | Set up virtual NAT, bridges, and isolated networks.                        |
| Security                   | Applies SELinux, AppArmor, sVirt isolation rules.                          |
| Remote Access              | Exposes TCP/TLS/SSH sockets for remote control (`qemu+ssh`, etc.).         |
| Authentication             | Supports UNIX sockets, SASL, TLS certificates for secure access.           |

---

## Service and Socket Management

### Systemd Units

```bash
systemctl status libvirtd.service
systemctl enable libvirtd.service
systemctl restart libvirtd.service
```

Also includes:

```bash
libvirtd.socket         # UNIX socket for local connections
libvirtd-ro.socket      # Read-only socket
libvirtd-admin.socket   # Administrative operations
```

---

## Configuration Files

| File                                  | Purpose                                         |
|---------------------------------------|-------------------------------------------------|
| `/etc/libvirt/libvirtd.conf`         | Core daemon settings (logging, sockets, etc.)   |
| `/etc/sysconfig/libvirtd` (RPM)      | Environment variables for daemon (old distros)  |
| `/etc/libvirt/qemu.conf`             | QEMU/KVM specific settings                      |

---

## Key `libvirtd.conf` Options

```conf
listen_tls = 1
listen_tcp = 1
auth_unix_rw = "polkit"
unix_sock_group = "libvirt"
unix_sock_rw_perms = "0770"
```

Use `virt-manager`, `virsh`, or custom clients to interact with `libvirtd`.

---

## Logging and Debugging

Enable debug mode:

```bash
LIBVIRT_DEBUG=1 LIBVIRT_LOG_OUTPUTS=1:file:/tmp/libvirt.log virsh list
```

Or increase verbosity in `/etc/libvirt/libvirtd.conf`:

```conf
log_level = 1
log_outputs="1:file:/var/log/libvirt/libvirtd.log"
```

Then:

```bash
systemctl restart libvirtd
```

---

## Replacement in Modern Setups

| Old (`libvirtd`)        | New (modular daemons)   |
|--------------------------|--------------------------|
| `libvirtd`               | `virtqemud`, `virtlogd`, `virtproxyd`, etc. |
| `/var/run/libvirtd/`     | `/run/libvirt/qemu/`, `/run/libvirt/virtqemud/` |

You can switch to **modular mode** by stopping `libvirtd` and enabling individual daemons:

```bash
systemctl disable libvirtd
systemctl enable virtqemud virtlogd virtnetworkd
```

---

## Remote Access

Enable remote TCP/TLS connections:

1. In `/etc/libvirt/libvirtd.conf`:

```conf
listen_tcp = 1
listen_tls = 1
auth_tcp = "sasl"
```

2. In `/etc/default/libvirtd` or systemd override:

```bash
LIBVIRTD_ARGS="--listen"
```

Then:

```bash
systemctl restart libvirtd
```

Connect using:

```bash
virsh -c qemu+ssh://user@host/system
```

---

## Summary

| Component    | Purpose                                  |
|--------------|------------------------------------------|
| `libvirtd`   | Main legacy libvirt daemon               |
| Manages      | VMs, networks, storage, hypervisor APIs  |
| Interface    | Sockets (UNIX/TCP), RPC protocol          |
| Security     | SELinux, TLS, SASL, UNIX auth            |
| Status       | Deprecated in favor of modular daemons   |

---

Let me know if you'd like a guide to **migrating from `libvirtd` to modular daemons**, configuring remote access securely, or benchmarking libvirt vs. competitors like `virt-manager`, `cockpit`, `xen-tools`, or `VBoxManage`.
