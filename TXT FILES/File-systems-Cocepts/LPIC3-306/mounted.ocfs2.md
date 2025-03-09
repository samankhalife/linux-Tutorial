# mounted.ocfs2
The `mounted.ocfs2` command is used to display information about the **currently mounted OCFS2 (Oracle Cluster File System 2)** file systems on a system. It helps administrators quickly identify which OCFS2 file systems are mounted, along with important details like the device names, mount points, and file system labels.

### Purpose

- **List Mounted OCFS2 File Systems**:  
  Displays all the currently mounted OCFS2 file systems on the system.
  
- **Show Device Information**:  
  Shows details such as the block device, the file system's mount point, and the label (if set).

- **Provide Quick System Overview**:  
  Offers a quick overview of OCFS2 file systems for system administrators managing clustered environments.

### Basic Syntax

```bash
mounted.ocfs2 [OPTIONS]
```

### Common Options

- **`-d` or `--details`**:  
  Show detailed information about the mounted OCFS2 file systems, including the mount options, node information, and UUID.

  Example:
  ```bash
  mounted.ocfs2 --details
  ```

- **`-h` or `--help`**:  
  Display help information about the `mounted.ocfs2` command and its usage.

  Example:
  ```bash
  mounted.ocfs2 --help
  ```

- **`-V` or `--version`**:  
  Show the version of the `mounted.ocfs2` utility.

  Example:
  ```bash
  mounted.ocfs2 --version
  ```

### Example Usage

1. **List Mounted OCFS2 File Systems**

   To list all currently mounted OCFS2 file systems:

   ```bash
   mounted.ocfs2
   ```

   This will display the block device and the mount point for each mounted OCFS2 file system.

2. **Show Detailed Information**

   To show more detailed information, including mount options and node-specific details:

   ```bash
   mounted.ocfs2 --details
   ```

   This will provide a more comprehensive view of the mounted OCFS2 file systems, including cluster-specific details.

### Example Output

Here’s an example of the output you might see when running `mounted.ocfs2`:

```bash
Device: /dev/sdb1
Mount Point: /mnt/ocfs2
Label: MyClusterFS
UUID: 11111111-2222-3333-4444-555555555555
Mount Options: rw,relatime
Number of Nodes: 4
```

This shows the device name, mount point, file system label, UUID, and mount options for a mounted OCFS2 file system, along with the number of nodes currently in the cluster.

### Best Practices

- **Regular Monitoring**:  
  Use `mounted.ocfs2` regularly to ensure that all OCFS2 file systems are mounted correctly, especially in multi-node cluster environments.

- **Check for Mount Issues**:  
  If you suspect a mount issue or file system misconfiguration, use `mounted.ocfs2 --details` to gather detailed information and troubleshoot.

- **Validate Cluster Nodes**:  
  For cluster environments, ensure that the number of nodes displayed matches the expected configuration to avoid potential issues with file system access and performance.

### Conclusion

The `mounted.ocfs2` utility is a simple yet essential tool for administrators working with OCFS2 file systems. It provides quick insight into which OCFS2 file systems are mounted, along with important details that can aid in system management and troubleshooting in cluster environments.
