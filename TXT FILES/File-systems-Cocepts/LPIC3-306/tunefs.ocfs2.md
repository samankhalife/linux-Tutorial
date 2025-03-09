# tunefs.ocfs2

The `tunefs.ocfs2` command is used to **modify file system parameters** on an existing OCFS2 (Oracle Cluster File System 2) file system. It allows system administrators to fine-tune various settings on the file system, such as enabling or disabling features, changing cluster information, and adjusting the size of certain structures within the file system.

### Purpose

- **Adjust File System Parameters**:  
  Modify file system parameters after the file system has been created.
  
- **Enable/Disable Features**:  
  Enable or disable features like unwritten extents, inline data, and backup superblocks.

- **Tune Cluster Settings**:  
  Adjust cluster-related settings such as heartbeat or quorum behavior.

### Basic Syntax

```bash
tunefs.ocfs2 [OPTIONS] <DEVICE>
```

- **`<DEVICE>`**: The block device containing the OCFS2 file system to be modified (e.g., `/dev/sdb1`).

### Common Options

- **`-L` or `--label`**:  
  Change the file system label. This is useful for identifying file systems by name rather than by device name.

  Example:
  ```bash
  tunefs.ocfs2 -L "NewLabel" /dev/sdb1
  ```

- **`-N` or `--nodes`**:  
  Set the maximum number of nodes that can mount the OCFS2 file system. OCFS2 supports concurrent access by multiple nodes, and this option adjusts the maximum number of nodes allowed.

  Example:
  ```bash
  tunefs.ocfs2 -N 8 /dev/sdb1
  ```

- **`-q` or `--query`**:  
  Query the file system for its current configuration, such as the number of nodes, the block size, and enabled features.

  Example:
  ```bash
  tunefs.ocfs2 -q /dev/sdb1
  ```

- **`-U` or `--uuid`**:  
  Change the UUID of the file system. The UUID is a unique identifier for the file system and can be useful for distinguishing between multiple OCFS2 file systems.

  Example:
  ```bash
  tunefs.ocfs2 -U <new-uuid> /dev/sdb1
  ```

- **`--fs-features`**:  
  Enable or disable specific file system features. For example, you can enable support for unwritten extents or inline data.

  Example:
  ```bash
  tunefs.ocfs2 --fs-features=unwritten /dev/sdb1
  ```

  To disable a feature:
  ```bash
  tunefs.ocfs2 --fs-features=noinline-data /dev/sdb1
  ```

- **`-J` or `--journal-options`**:  
  Tune the journal options, such as changing the size of the journal or adding new journals.

  Example:
  ```bash
  tunefs.ocfs2 -J size=64M /dev/sdb1
  ```

- **`-b` or `--backup-superblocks`**:  
  Enable or disable backup superblocks. Backup superblocks provide redundancy in case the main superblock becomes corrupted.

  Example:
  ```bash
  tunefs.ocfs2 --backup-superblocks /dev/sdb1
  ```

- **`--no-heartbeat`**:  
  Disable heartbeat for the OCFS2 file system. Heartbeat is typically used in clustered environments to monitor node health, but it can be disabled if it's unnecessary.

  Example:
  ```bash
  tunefs.ocfs2 --no-heartbeat /dev/sdb1
  ```

### Example Usage

1. **Query the File System Configuration**

   To display the current configuration of an OCFS2 file system:

   ```bash
   tunefs.ocfs2 -q /dev/sdb1
   ```

   This will output information such as the block size, cluster size, maximum number of nodes, and enabled file system features.

2. **Set a New Label for the File System**

   To assign a new label (name) to an OCFS2 file system:

   ```bash
   tunefs.ocfs2 -L "MyClusterFS" /dev/sdb1
   ```

   This can be useful for distinguishing between different file systems on the same system.

3. **Change the Maximum Number of Nodes**

   To increase the maximum number of nodes allowed to mount the OCFS2 file system:

   ```bash
   tunefs.ocfs2 -N 16 /dev/sdb1
   ```

   This adjusts the file system to support up to 16 nodes concurrently mounting the file system.

4. **Enable Unwritten Extents**

   To enable support for unwritten extents on the file system (a feature that allows preallocation of blocks without initializing them):

   ```bash
   tunefs.ocfs2 --fs-features=unwritten /dev/sdb1
   ```

5. **Disable Inline Data Support**

   To disable support for inline data, which stores small files directly within inodes to reduce overhead:

   ```bash
   tunefs.ocfs2 --fs-features=noinline-data /dev/sdb1
   ```

6. **Resize the Journal**

   To increase the size of the journal on the OCFS2 file system (useful for improving performance under heavy write loads):

   ```bash
   tunefs.ocfs2 -J size=128M /dev/sdb1
   ```

### Example Output

Here’s an example of what you might see when querying the file system configuration with `tunefs.ocfs2`:

```bash
tunefs.ocfs2 1.8.6
Label: MyClusterFS
UUID: 11111111-2222-3333-4444-555555555555
Number of nodes: 8
Block size: 4096
Cluster size: 65536
Journal size: 64M
Features: backup-superblocks unwritten inline-data
```

This output shows the current label, UUID, number of nodes, block size, cluster size, journal size, and enabled features of the OCFS2 file system.

### Best Practices

- **Check the Current Configuration Before Making Changes**:  
  Always use the `-q` option to check the current configuration before making any changes to the file system. This allows you to see the current state and ensure that your changes are appropriate.

- **Use Backup Superblocks**:  
  Enable backup superblocks (`--backup-superblocks`) to provide redundancy in case the main superblock becomes corrupted. This can help in recovering the file system in case of failure.

- **Adjust Node Count as Needed**:  
  Ensure the maximum number of nodes (`-N`) is set appropriately for your cluster environment. If you expect to add more nodes in the future, it's a good idea to configure the file system to handle that many nodes in advance.

- **Tune Journal Size Based on Write Load**:  
  If your OCFS2 file system handles a high volume of write operations, consider increasing the size of the journal (`-J`) to improve performance.

- **Backup Important Data**:  
  Before making any significant changes to the file system, such as enabling or disabling features, always ensure that you have a backup of your important data.

### Conclusion

The `tunefs.ocfs2` command is a powerful tool for tuning and modifying the parameters of an OCFS2 file system. It allows administrators to enable or disable file system features, adjust node counts, and modify other file system characteristics after the file system has been created. Proper use of `tunefs.ocfs2` can enhance the performance and reliability of OCFS2 in clustered environments.
