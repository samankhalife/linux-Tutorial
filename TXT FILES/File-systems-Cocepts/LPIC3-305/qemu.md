# `qemu` — Quick Emulator

## What is QEMU?

QEMU (Quick Emulator) is an open-source emulator and virtualizer that allows you to run virtual machines (VMs) on a host system. It can emulate various hardware architectures (such as x86, ARM, PowerPC, and others) and provides a flexible platform for testing and development.

QEMU is widely used for system emulation, virtual machine creation, and running virtual environments. It supports full system emulation, where the CPU and peripheral devices of a system are emulated, as well as user-mode emulation, which allows running executables built for one architecture on another architecture.

---

## Key Features of QEMU

- **Architecture Support**: Emulates a wide range of CPU architectures (e.g., x86, ARM, MIPS, PowerPC, RISC-V, and others).
- **Full System Emulation**: Supports emulation of a complete system with virtualized hardware (e.g., memory, CPU, disk, and network devices).
- **User-Mode Emulation**: Allows running programs built for different architectures on your native architecture.
- **Snapshotting**: Supports VM snapshots, which allow you to save and restore the state of a virtual machine.
- **Live Migration**: Can migrate a running virtual machine from one host to another without downtime.
- **KVM Support**: Works with Linux Kernel-based Virtual Machine (KVM) for improved performance when running on supported hardware.
- **Virtualization**: Supports both hardware and software-based virtualization for guest systems.
- **Networking**: Provides multiple networking options, including tap, bridge, and user-mode networking.
- **Disk I/O**: Supports various disk formats like `qcow2`, `raw`, `vmdk`, and others.

---

## Common Commands

### Basic Syntax

```bash
qemu [options] [disk-image] [other-options]
```

Where:
- **[options]** are the command-line options for QEMU (e.g., CPU architecture, memory size).
- **[disk-image]** refers to the virtual disk image for the VM.
- **[other-options]** are additional arguments (e.g., networking, display options).

---

## Commonly Used `qemu` Commands

### 1. **Start a Virtual Machine**

To start a VM with a specific disk image and virtual hardware options:

```bash
qemu-system-x86_64 -hda /path/to/disk-image.qcow2 -m 2048
```

- **`qemu-system-x86_64`**: Specifies the architecture (e.g., x86_64 for 64-bit x86 systems).
- **`-hda`**: Specifies the disk image (e.g., `/path/to/disk-image.qcow2`).
- **`-m 2048`**: Allocates 2 GB of memory to the VM.

### 2. **Running a Virtual Machine with Multiple CPUs**

```bash
qemu-system-x86_64 -hda /path/to/disk-image.qcow2 -m 2048 -smp 4
```

- **`-smp 4`**: Allocates 4 virtual CPUs to the VM.

### 3. **Enable KVM for Hardware Acceleration**

For improved performance, you can use KVM (Kernel-based Virtual Machine) for hardware acceleration (ensure KVM is supported and enabled on your host):

```bash
qemu-system-x86_64 -hda /path/to/disk-image.qcow2 -m 2048 -enable-kvm
```

### 4. **Create a Virtual Machine with a Network Interface**

To enable network interfaces in the virtual machine:

```bash
qemu-system-x86_64 -hda /path/to/disk-image.qcow2 -m 2048 -net nic -net user
```

- **`-net nic`**: Adds a network interface card (NIC) to the VM.
- **`-net user`**: Configures user-mode networking.

### 5. **Running a VM with Serial Console Output**

To redirect the console output of the VM to a serial port:

```bash
qemu-system-x86_64 -hda /path/to/disk-image.qcow2 -m 2048 -serial mon:stdio
```

- **`-serial mon:stdio`**: Redirects the serial console to the terminal.

### 6. **Using Virtual Disk Images**

Create a new virtual disk image:

```bash
qemu-img create -f qcow2 /path/to/new-image.qcow2 10G
```

- **`qemu-img create`**: Creates a new disk image.
- **`-f qcow2`**: Specifies the format of the disk image (e.g., `qcow2` is the QEMU copy-on-write format).
- **`10G`**: Specifies the size of the virtual disk image (10 GB).

### 7. **Run a Virtual Machine with a CD-ROM or ISO Image**

To boot the virtual machine from an ISO image:

```bash
qemu-system-x86_64 -cdrom /path/to/iso-file.iso -m 2048 -boot d
```

- **`-cdrom /path/to/iso-file.iso`**: Specifies the ISO image file to boot from.
- **`-boot d`**: Tells QEMU to boot from the CD-ROM (ISO).

### 8. **Take a Snapshot of a VM**

Take a snapshot of the VM to save its state:

```bash
qemu-img snapshot -c snapshot-name /path/to/disk-image.qcow2
```

- **`snapshot -c snapshot-name`**: Creates a snapshot with the given name.

### 9. **Live Migration of a Virtual Machine**

To migrate a running VM from one host to another:

```bash
qemu-system-x86_64 -m 2048 -live-migration tcp:destination_host:port
```

- **`-live-migration`**: Enables live migration.
- **`tcp:destination_host:port`**: Specifies the destination for migration.

---

## Use Cases of QEMU

### Use Case 1: Testing Different Architectures

QEMU is widely used to test applications or operating systems on different hardware architectures. For example, you can test an ARM-based OS image on an x86 host.

```bash
qemu-system-arm -m 512 -M versatilepb -kernel /path/to/arm-kernel -append "root=/dev/sda1"
```

### Use Case 2: Running Virtual Machines on Non-Virtualization Hosts

Even if your host machine doesn't have hardware virtualization support (i.e., no Intel VT or AMD-V), QEMU can still run virtual machines using software emulation. This is useful for running legacy systems or testing specific use cases.

### Use Case 3: Running Operating Systems on Virtualized Hosts

With KVM acceleration enabled, QEMU can be used to run virtual machines with minimal overhead on systems that support hardware virtualization.

---

## Comparison with Other Virtualization Tools

| Feature               | QEMU                                      | VirtualBox                       | VMware                          |
|-----------------------|-------------------------------------------|----------------------------------|---------------------------------|
| Architecture Support   | Multiple architectures (x86, ARM, etc.)   | Limited (mostly x86)             | Limited (mostly x86)            |
| KVM Support            | Yes (for Linux hosts)                     | No                               | Yes (for Linux hosts)           |
| Snapshot Support       | Yes                                       | Yes                              | Yes                             |
| Live Migration         | Yes                                       | No                               | Yes                             |
| Performance            | High (with KVM acceleration)              | Moderate                         | High                            |

---

## Disk Formats Supported by QEMU

- **`qcow2`**: The default disk format, supports snapshots and compression.
- **`raw`**: A simple format that represents the raw contents of a disk, typically used for compatibility.
- **`vmdk`**: VMware disk format, used to import/export from VMware products.
- **`vdi`**: VirtualBox disk format.

---

## Summary

| Feature               | QEMU                                    |
|-----------------------|-----------------------------------------|
| Purpose               | Virtual machine and system emulator     |
| Common Use Cases      | Testing various OS and architectures, virtualization, disk image management |
| Supported Architectures | x86, ARM, PowerPC, RISC-V, and others   |
| Popular Commands      | `qemu-system`, `qemu-img`, `qemu-nbd`    |
| Comparison            | More flexible than VirtualBox and VMware for architecture testing and full system emulation |

---

QEMU is an essential tool for system emulation and virtualization, widely used for development, testing, and learning purposes across various hardware platforms. It is highly customizable, supports multiple architectures, and, when paired with KVM, offers great performance for virtual machines on Linux.
