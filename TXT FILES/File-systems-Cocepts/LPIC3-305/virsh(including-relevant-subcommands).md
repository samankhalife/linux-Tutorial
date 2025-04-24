# `virsh` — Virtualization Shell for Managing VMs

`virsh` is a command-line interface for managing virtual machines via **libvirt**, typically used with **KVM**, **QEMU**, and other virtualization technologies. It supports operations like VM lifecycle management, storage, network, snapshots, and resource monitoring.

---

## Key Features

- **Lifecycle Management**: Start, stop, suspend, and destroy VMs.
- **Persistent and Transient VMs**: Manage both runtime and saved configurations.
- **Storage and Networking**: Control virtual disks, volumes, and virtual networks.
- **Snapshots**: Create and revert to VM snapshots.
- **Remote Management**: Manage VMs on remote hosts over SSH or TLS.
- **Interactive and Non-interactive Use**: Run commands or enter an interactive shell.

---

## Basic Syntax

```bash
virsh [options] <command> [args]
```

Example:

```bash
virsh start vm-name
```

---

## Common and Essential Subcommands

### 1. **VM Lifecycle Management**

- **List VMs (running or all)**

  ```bash
  virsh list          # Only running
  virsh list --all    # All domains (running + shut off)
  ```

- **Start / Shutdown / Destroy / Reboot**

  ```bash
  virsh start vm-name
  virsh shutdown vm-name
  virsh destroy vm-name        # Force off (like pulling power plug)
  virsh reboot vm-name
  ```

- **Suspend / Resume**

  ```bash
  virsh suspend vm-name
  virsh resume vm-name
  ```

- **Autostart on Boot**

  ```bash
  virsh autostart vm-name
  virsh autostart --disable vm-name
  ```

---

### 2. **Domain and Resource Info**

- **Get VM Information**

  ```bash
  virsh dominfo vm-name
  virsh domuuid vm-name
  virsh domstate vm-name
  ```

- **CPU and Memory Statistics**

  ```bash
  virsh dommemstat vm-name
  virsh domstats vm-name
  ```

---

### 3. **VM Configuration and XML**

- **Dump or Edit XML Configuration**

  ```bash
  virsh dumpxml vm-name         # Show XML
  virsh edit vm-name            # Edit XML with $EDITOR
  ```

- **Define or Undefine Domains**

  ```bash
  virsh define vm.xml           # Create from XML
  virsh undefine vm-name        # Remove config only
  ```

---

### 4. **Snapshot Management**

- **Create and Manage Snapshots**

  ```bash
  virsh snapshot-create-as vm-name snap1 "Snapshot description"
  virsh snapshot-list vm-name
  virsh snapshot-revert vm-name --snapshotname snap1
  virsh snapshot-delete vm-name --snapshotname snap1
  ```

---

### 5. **Console and Access**

- **Connect to Serial Console**

  ```bash
  virsh console vm-name
  ```

  To exit: `Ctrl+]`

---

### 6. **Storage Management**

- **List, Create, and Delete Volumes**

  ```bash
  virsh vol-list default
  virsh vol-create-as default vol1.img 10G
  virsh vol-delete vol1.img --pool default
  ```

- **Pool Management**

  ```bash
  virsh pool-list
  virsh pool-start default
  virsh pool-refresh default
  ```

---

### 7. **Network Management**

- **List, Start, and Define Networks**

  ```bash
  virsh net-list --all
  virsh net-start default
  virsh net-destroy default
  virsh net-define net.xml
  virsh net-autostart default
  ```

---

### 8. **Remote and Interactive Mode**

- **Connect to Remote Host**

  ```bash
  virsh -c qemu+ssh://user@remote/system
  ```

- **Enter Interactive Shell**

  ```bash
  virsh
  ```

---

## Example Use Cases

### Start a Virtual Machine

```bash
virsh start ubuntu-vm
```

---

### Check Running VMs

```bash
virsh list
```

---

### Create a Snapshot Before Upgrade

```bash
virsh snapshot-create-as ubuntu-vm pre-upgrade "Before system upgrade"
```

---

### Attach a CD-ROM ISO Image

```bash
virsh attach-disk ubuntu-vm /isos/ubuntu.iso hdc --type cdrom --mode readonly
```

---

## Conclusion

`virsh` is an indispensable tool for Linux-based virtualization environments using libvirt. It provides complete lifecycle control, resource introspection, and management capabilities for virtual machines, networks, and storage — both locally and remotely. It’s highly scriptable and favored for automation and infrastructure orchestration workflows.
