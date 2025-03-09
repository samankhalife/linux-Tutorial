# o2info
The `o2info` command is part of the **OCFS2 (Oracle Cluster File System 2)** tools suite and is used to display detailed information about a mounted OCFS2 file system. It provides insights into various aspects of the file system, including superblock information, cluster layout, and other metadata details.

### Purpose

- **Inspect OCFS2 File System Details**:  
  `o2info` provides detailed information about the structure and metadata of an OCFS2 file system, which is useful for both debugging and monitoring purposes.
  
- **Superblock Inspection**:  
  It allows administrators to inspect the OCFS2 superblock, a key component that contains the file system's metadata.

- **Cluster Information**:  
  Shows information about the cluster nodes involved with the OCFS2 file system, which is crucial in a clustered environment.

### Basic Syntax

```bash
o2info [OPTIONS] <MOUNT_POINT>
```

- **`<MOUNT_POINT>`**: The path where the OCFS2 file system is mounted.

### Common Options

- **`-s` or `--superblock`**:  
  Display detailed information about the superblock of the OCFS2 file system.

  Example:
  ```bash
  o2info --superblock /mnt/ocfs2
  ```

- **`-C` or `--cluster`**:  
  Display detailed cluster layout and node information for the OCFS2 file system.

  Example:
  ```bash
  o2info --cluster /mnt/ocfs2
  ```

- **`-h` or `--help`**:  
  Display help information about the command.

  Example:
  ```bash
  o2info --help
  ```

- **`-V` or `--version`**:  
  Display the version of `o2info`.

  Example:
  ```bash
  o2info --version
  ```

### Example Usage

1. **Viewing Superblock Information**

   To view detailed superblock information for an OCFS2 file system mounted at `/mnt/ocfs2`:

   ```bash
   o2info --superblock /mnt/ocfs2
   ```

   This will display important superblock data, such as block size, cluster size, UUID, and more.

2. **Viewing Cluster Layout and Node Information**

   To display the cluster information for an OCFS2 file system mounted at `/mnt/ocfs2`:

   ```bash
   o2info --cluster /mnt/ocfs2
   ```

   This will show the nodes participating in the OCFS2 cluster, their roles, and the current status.

### Example Output

When running `o2info` to view superblock information, you may see output like this:

```bash
Superblock Information
-----------------------
Block Size: 4096
Cluster Size: 65536
Volume UUID: 12345678-90ab-cdef-1234-567890abcdef
Volume Label: MyClusterFS
Node Slots: 8
```

For cluster information, the output may look like this:

```bash
Cluster Information
--------------------
Cluster Name: ocfs2_cluster
Node Count: 3
Node 1: Online
Node 2: Online
Node 3: Online
```

### Best Practices

- **Monitor File System Health**:  
  Use `o2info --superblock` regularly to check the health and consistency of the superblock on your OCFS2 file systems.

- **Cluster Node Management**:  
  Check the cluster layout and node information using `o2info --cluster` to ensure all nodes in the cluster are communicating and functioning properly.

- **Troubleshooting**:  
  Use the detailed output from `o2info` to assist in diagnosing file system or cluster-related issues.

### Conclusion

`o2info` is a valuable tool for administrators managing OCFS2 file systems in clustered environments. It provides critical information about the file system's superblock and cluster configuration, aiding in file system monitoring, debugging, and management.
