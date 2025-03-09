# mount.ocfs2

The `mount.ocfs2` command is used to mount **OCFS2 (Oracle Cluster File System 2)** file systems on a device to a specified mount point. This command is essential for enabling access to OCFS2 file systems, which are designed to be shared across multiple nodes in a cluster.

OCFS2 supports concurrent read and write operations across nodes, making it useful for environments where data consistency and availability are critical, such as Oracle database clusters.

### Purpose

- **Mount OCFS2 File System**:  
  This command mounts an OCFS2 file system to a directory on a local node, enabling access to the files on the shared storage.
  
- **Cluster-Aware Mounting**:  
  The `mount.ocfs2` command coordinates with the OCFS2 cluster stack to manage concurrent access to the file system by different nodes.

### Basic Syntax

```bash
mount.ocfs2 [OPTIONS] <DEVICE> <MOUNT_POINT>
```

- **`<DEVICE>`**: The block device or partition containing the OCFS2 file system (e.g., `/dev/sdb1`).
- **`<MOUNT_POINT>`**: The directory where the file system will be mounted (e.g., `/mnt/ocfs2`).

### Common Options

- **`-o` or **`--options`**:  
  Mount the file system with specific options. This can include options such as `ro` for read-only, `noatime` to disable access time updates, or `acl` to enable access control lists.

  Example:
  ```bash
  mount.ocfs2 -o acl /dev/sdb1 /mnt/ocfs2
  ```

- **`-r`** or **`--read-only`**:  
  Mount the file system in read-only mode. This prevents write operations, ensuring that data is not modified on the shared file system.

  Example:
  ```bash
  mount.ocfs2 -r /dev/sdb1 /mnt/ocfs2
  ```

- **`-t`** or **`--type`**:  
  Specify the file system type. While `mount.ocfs2` is designed for OCFS2, this option allows you to explicitly specify `ocfs2` as the file system type.

  Example:
  ```bash
  mount.ocfs2 -t ocfs2 /dev/sdb1 /mnt/ocfs2
  ```

- **`-o datavolume`**:  
  If the OCFS2 volume is a data volume (not intended for metadata or Oracle RAC voting disks), you can use the `datavolume` option.

  Example:
  ```bash
  mount.ocfs2 -o datavolume /dev/sdb1 /mnt/ocfs2
  ```

- **`-o nointr`**:  
  Prevent system calls from being interrupted. Useful for preventing unwanted interruptions during file system operations.

  Example:
  ```bash
  mount.ocfs2 -o nointr /dev/sdb1 /mnt/ocfs2
  ```

### Example Usage

1. **Mounting an OCFS2 File System**

   To mount an OCFS2 file system on `/dev/sdb1` to `/mnt/ocfs2`:

   ```bash
   mount.ocfs2 /dev/sdb1 /mnt/ocfs2
   ```

   This command mounts the OCFS2 file system located on `/dev/sdb1` to the directory `/mnt/ocfs2` for access.

2. **Mounting an OCFS2 File System as Read-Only**

   If you want to mount the OCFS2 file system in read-only mode:

   ```bash
   mount.ocfs2 -r /dev/sdb1 /mnt/ocfs2
   ```

   This will prevent any write operations on the mounted file system.

3. **Mounting with Specific Options**

   To mount with access control lists (ACLs) enabled and disable access time updates:

   ```bash
   mount.ocfs2 -o acl,noatime /dev/sdb1 /mnt/ocfs2
   ```

4. **Mounting a Data Volume**

   To mount the device as a data volume (typically used in Oracle environments for data disks):

   ```bash
   mount.ocfs2 -o datavolume /dev/sdb1 /mnt/ocfs2
   ```

### Automating Mount with `/etc/fstab`

You can add an entry in the `/etc/fstab` file to automatically mount an OCFS2 file system on boot.

Example:

```bash
/dev/sdb1    /mnt/ocfs2    ocfs2    defaults,_netdev    0 0
```

This will mount `/dev/sdb1` as an OCFS2 file system to `/mnt/ocfs2` on system boot.

### Example Output

When you mount an OCFS2 file system, the output is typically minimal, but you can check the mounted file systems using the `mount` command or by examining `/proc/mounts`:

```bash
$ mount | grep ocfs2
/dev/sdb1 on /mnt/ocfs2 type ocfs2 (rw)
```

### Best Practices

- **Cluster Node Configuration**:  
  Ensure that all nodes in the cluster are correctly configured to use OCFS2, and that they can access the shared storage. Each node in the cluster should have the OCFS2 tools installed and configured.

- **Backup Critical Data**:  
  Since OCFS2 is a shared file system, concurrent write access can increase the risk of data corruption if something goes wrong. Always back up critical data before making significant changes.

- **File System Checks**:  
  Regularly check the file system's health with `fsck.ocfs2` to ensure that the file system remains consistent, especially after a node failure or unclean shutdown.

- **Permissions and ACLs**:  
  If your use case requires fine-grained file access control, enable ACLs when mounting the file system to allow for detailed user permissions management.

- **Ensure Cluster Daemons are Running**:  
  Make sure that OCFS2 cluster services, such as `o2cb` (OCFS2 Cluster Base), are running before mounting the file system on any node in the cluster.

### Conclusion

The `mount.ocfs2` command is a critical tool for accessing OCFS2 file systems in shared, clustered environments. By mounting the file system with appropriate options, you can ensure proper access control, optimize performance, and maintain consistency across multiple nodes. As with any clustered file system, it is essential to carefully manage access and monitor the system to avoid data corruption and ensure high availability.
