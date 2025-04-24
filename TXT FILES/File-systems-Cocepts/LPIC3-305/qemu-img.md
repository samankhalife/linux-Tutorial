# `qemu-img` — QEMU Disk Image Utility

`qemu-img` is a powerful command-line utility included with QEMU (Quick EMUlator), used to create, convert, inspect, resize, and manage disk image files. It supports various formats and is commonly used in virtualization workflows involving KVM, QEMU, libvirt, or cloud image preparation.

---

## Key Features

- **Create and Convert Disk Images**: Supports multiple formats like `qcow2`, `raw`, `vmdk`, `vdi`, `vhd`, etc.
- **Inspect Disk Image Info**: Displays format, virtual size, actual size, backing files, and more.
- **Resize and Modify Images**: Extend or shrink image sizes, adjust formats, or preallocate space.
- **Snapshot and Backing File Support**: Works with layered images using base files and copy-on-write.
- **Efficient Compression and Sparsification**: Reduce image size for storage or distribution.

---

## Basic Syntax

```bash
qemu-img <command> [options]
```

---

## Common Commands

### Create a New Disk Image

```bash
qemu-img create -f qcow2 disk.qcow2 20G
```

Creates a 20 GB image in `qcow2` format.

---

### Convert Between Formats

```bash
qemu-img convert -f raw -O qcow2 disk.raw disk.qcow2
```

Converts a raw image to `qcow2`.

---

### Display Image Information

```bash
qemu-img info disk.qcow2
```

Shows details such as format, virtual size, and backing files.

---

### Resize a Disk Image

```bash
qemu-img resize disk.qcow2 +5G
```

Expands the disk image size by 5 GB.

---

### Check Image Integrity

```bash
qemu-img check disk.qcow2
```

Performs a consistency check to detect errors in the image.

---

### Compress a Disk Image

```bash
qemu-img convert -O qcow2 -c disk.raw disk-compressed.qcow2
```

Converts and compresses the image.

---

## Supported Formats

- `qcow2`: QEMU Copy-On-Write (default for QEMU/KVM)
- `raw`: Unformatted binary image
- `vmdk`: VMware disk format
- `vhd` / `vhdx`: Hyper-V
- `vdi`: VirtualBox format
- `luks`: Encrypted image
- Others supported via plugins or drivers

---

## Example Use Cases

### Cloud Image Preparation

Convert cloud-init images or shrink images for minimal cloud deployments:

```bash
qemu-img convert -O qcow2 cloud.img prepared-cloud.qcow2
```

---

### Snapshot Workflows

Combine with `backing_file` for snapshot-based workflows:

```bash
qemu-img create -f qcow2 -b base.qcow2 snapshot.qcow2
```

Creates a copy-on-write snapshot from a base image.

---

### Disk Image Shrinking (Zero out unused space first)

```bash
qemu-img convert -O qcow2 disk.qcow2 disk-shrink.qcow2
```

Reduces the size of the image file if it's sparse.

---

## Example Output

```bash
qemu-img info disk.qcow2
image: disk.qcow2
file format: qcow2
virtual size: 20G (21474836480 bytes)
disk size: 1.5G
cluster_size: 65536
backing file: base.qcow2
```

---

## Use Case Scenarios

- **Automation and CI/CD**: Automate creation and conversion of disk images in CI pipelines.
- **Virtualization Infrastructure**: Prepare VM images for KVM, libvirt, or cloud deployment.
- **Forensics and Testing**: Duplicate or analyze disk contents without modifying originals.
- **Snapshot Chains and Rollbacks**: Manage base images and snapshots for test environments.

---

## Conclusion

`qemu-img` is an essential tool for managing virtual disk images in QEMU/KVM environments. With robust support for various image formats, snapshot management, conversion, and resizing features, it is critical in both development and production scenarios involving virtualization, cloud deployment, and image management.
