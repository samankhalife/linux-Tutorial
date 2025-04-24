`virt-inspector` is a command-line utility that is part of the **libvirt** suite, specifically designed to inspect virtual machine (VM) disk images. It allows administrators to view detailed information about the contents of virtual disk images, including filesystems, partitions, and other metadata without needing to boot the virtual machine.

This tool is particularly useful for system administrators and those working in virtualized environments, as it allows inspection of VM disk images offline. It can read disk image formats like `qcow2`, `raw`, and `vmdk`, among others.

### Key Features of `virt-inspector`

- **Inspect Virtual Machine Disk Images**: Provides an easy way to inspect the contents of virtual machine disk images.
- **View Partition Tables**: Displays partition tables and information about individual partitions within the disk image.
- **Filesystem Information**: Shows detailed filesystem information including filesystem types and mount points.
- **Metadata**: Can provide metadata about virtual disks, including labels, UUIDs, and other useful attributes.
- **Support for Multiple Disk Formats**: Works with multiple virtual disk formats, including `qcow2`, `raw`, `vmdk`, and others.
- **No Need for VM to Be Running**: You can inspect the disk image offline, without requiring the virtual machine to be running.

### Basic Syntax

```bash
virt-inspector [options] disk_image
```

- **disk_image**: The path to the virtual disk image you want to inspect.

### Common Options

- `-a, --add`: Add one or more disk images to the inspection.
- `-l, --long`: Provides a long listing format with more detailed information (such as filesystem type and sizes).
- `-m, --mount`: Display the mount points for each filesystem in the image.
- `-t, --type`: Filter the output by a specific type of filesystem (e.g., `ext4`, `xfs`).
- `-h, --help`: Displays help information for the command.

### Common Use Cases for `virt-inspector`

1. **Inspect the Disk Image of a Virtual Machine**

   To inspect a virtual machine disk image (e.g., `/path/to/disk-image.qcow2`), run:

   ```bash
   virt-inspector /path/to/disk-image.qcow2
   ```

   This will provide a summary of the disk image's contents, including partition table, filesystem types, and metadata.

2. **Display Detailed Information about Filesystems**

   To display detailed information about the filesystems in a virtual disk image, use the `-l` (long) option:

   ```bash
   virt-inspector -l /path/to/disk-image.qcow2
   ```

   This will show more detailed information, such as filesystem sizes and types.

3. **Inspect Filesystem Types**

   If you are interested in only certain types of filesystems (e.g., `ext4`), you can filter the output by filesystem type using the `-t` option:

   ```bash
   virt-inspector -t ext4 /path/to/disk-image.qcow2
   ```

   This will show only `ext4` filesystems in the disk image.

4. **View Partition Information**

   If you want to see partition information (such as sizes and types of partitions), you can use the `-l` option:

   ```bash
   virt-inspector -l /path/to/disk-image.qcow2
   ```

   **Output Example**:
   ```
   /dev/sda1: ext4, size: 100G, mount point: /
   /dev/sda2: swap, size: 4G, mount point: none
   ```

5. **Inspect a Running VM's Disk Image**

   To inspect the disk image of a running virtual machine, you can specify the domain (VM) name:

   ```bash
   virt-inspector --domain vm_name
   ```

   This will show the disk image information for the specified running VM.

### Example Output

- **Example 1**: Inspect a disk image (`disk-image.qcow2`):

   ```bash
   virt-inspector /path/to/disk-image.qcow2
   ```

   **Output**:
   ```
   Disk Image: /path/to/disk-image.qcow2
   Partition Table: GPT
   Filesystems:
   /dev/sda1: ext4, size: 100G, mount point: /
   /dev/sda2: swap, size: 4G, mount point: none
   ```

- **Example 2**: Detailed information about filesystems in a disk image:

   ```bash
   virt-inspector -l /path/to/disk-image.qcow2
   ```

   **Output**:
   ```
   Disk Image: /path/to/disk-image.qcow2
   Partition Table: GPT
   Filesystems:
   /dev/sda1: ext4, size: 100G, mount point: /
   /dev/sda2: swap, size: 4G, mount point: none
   ```

### Why Use `virt-inspector`?

- **Offline Inspection**: It allows you to inspect a virtual disk image without having to run the virtual machine, making it useful for diagnostics or backups.
- **Convenient Metadata**: You can quickly obtain metadata, partition layouts, and filesystem types, which can be helpful when planning migrations or performing audits.
- **Supports Multiple Formats**: It can handle a variety of disk image formats (such as `qcow2`, `raw`, `vmdk`), which is useful in diverse virtualization environments.
- **No Need for VM to Be Running**: This tool doesn't require the VM to be running, which is helpful if the VM is down or if you need to inspect the disk image offline.

### Conclusion

`virt-inspector` is an essential tool for inspecting virtual machine disk images, especially in virtualized environments managed with **libvirt**. It simplifies the process of querying detailed information about filesystems, partitions, and other metadata in a disk image without the need for the VM to be running. Whether you're performing backups, troubleshooting, or planning migrations, `virt-inspector` is a useful tool to quickly gather key details about virtual disks.
