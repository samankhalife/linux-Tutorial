# ceph-bluestore-tool 
`ceph-bluestore-tool` is a utility tool in Ceph used to inspect, repair, and manipulate **BlueStore** devices. BlueStore is the default storage backend for Ceph OSDs (Object Storage Daemons), optimized for modern solid-state drives (SSDs) and offering better performance compared to FileStore.



## Common `ceph-bluestore-tool` Commands and Subcommands

### 1. **fsck (Filesystem Check)**
Checks the integrity of the BlueStore OSD data, identifies inconsistencies, and optionally repairs them.

```bash
ceph-bluestore-tool fsck --path <path-to-osd> [--repair]
```

- Example:
  ```bash
  ceph-bluestore-tool fsck --path /var/lib/ceph/osd/ceph-1
  ```

This command checks the filesystem on the OSD at the specified path. Use the `--repair` flag to repair any issues found.

### 2. **repair**
Performs an in-depth repair on a BlueStore device. This is useful when an OSD fails due to data corruption.

```bash
ceph-bluestore-tool repair --path <path-to-osd>
```

- Example:
  ```bash
  ceph-bluestore-tool repair --path /var/lib/ceph/osd/ceph-1
  ```

This command performs a repair operation on the BlueStore OSD at `/var/lib/ceph/osd/ceph-1`.

### 3. **show-label**
Displays key information stored in the BlueStore OSD’s label, which includes metadata about the OSD such as its UUID.

```bash
ceph-bluestore-tool show-label --path <path-to-osd>
```

- Example:
  ```bash
  ceph-bluestore-tool show-label --path /var/lib/ceph/osd/ceph-1
  ```

This command shows the metadata stored on the label of the OSD.

### 4. **bluefs-bdev-sizes**
Displays the sizes of block devices used by **BlueFS**, a small file system used by BlueStore to store metadata.

```bash
ceph-bluestore-tool bluefs-bdev-sizes --path <path-to-osd>
```

- Example:
  ```bash
  ceph-bluestore-tool bluefs-bdev-sizes --path /var/lib/ceph/osd/ceph-1
  ```

This command prints the sizes of the block devices used by BlueFS in the specified OSD.

### 5. **bluefs-stats**
Displays statistics about BlueFS usage, including allocated and available space.

```bash
ceph-bluestore-tool bluefs-stats --path <path-to-osd>
```

- Example:
  ```bash
  ceph-bluestore-tool bluefs-stats --path /var/lib/ceph/osd/ceph-1
  ```

This command provides BlueFS usage statistics for the specified OSD.

### 6. **bluefs-bdev-replay**
Replays BlueFS logs to recover from corruption in the BlueFS metadata.

```bash
ceph-bluestore-tool bluefs-bdev-replay --path <path-to-osd>
```

- Example:
  ```bash
  ceph-bluestore-tool bluefs-bdev-replay --path /var/lib/ceph/osd/ceph-1
  ```

This command replays the BlueFS log to fix potential BlueFS metadata issues.

### 7. **rebuild-db**
Rebuilds the BlueStore RocksDB from scratch, which is used to store object metadata. It’s a more destructive operation but can be used if RocksDB gets corrupted.

```bash
ceph-bluestore-tool rebuild-db --path <path-to-osd>
```

- Example:
  ```bash
  ceph-bluestore-tool rebuild-db --path /var/lib/ceph/osd/ceph-1
  ```

This command completely rebuilds the OSD's RocksDB, which stores critical metadata about the objects.

### 8. **list-objects**
Lists the objects stored in the BlueStore database. This helps in inspecting the contents of the OSD.

```bash
ceph-bluestore-tool list-objects --path <path-to-osd>
```

- Example:
  ```bash
  ceph-bluestore-tool list-objects --path /var/lib/ceph/osd/ceph-1
  ```

This command lists all objects stored within the OSD's BlueStore.

### 9. **migrate-keyvaluedb-to-omap**
This subcommand migrates old key-value store entries to a newer OMAP format, necessary for performance improvements or consistency reasons in BlueStore.

```bash
ceph-bluestore-tool migrate-keyvaluedb-to-omap --path <path-to-osd>
```

- Example:
  ```bash
  ceph-bluestore-tool migrate-keyvaluedb-to-omap --path /var/lib/ceph/osd/ceph-1
  ```

This command migrates legacy key-value data to OMAP in the BlueStore OSD at the specified path.

### 10. **compact**
Compacts the RocksDB database to reduce space usage and improve performance by removing stale data and reorganizing on-disk structures.

```bash
ceph-bluestore-tool compact --path <path-to-osd>
```

- Example:
  ```bash
  ceph-bluestore-tool compact --path /var/lib/ceph/osd/ceph-1
  ```

This command compacts the RocksDB for the specified BlueStore OSD.



## Typical Use Cases:

1. **OSD Corruption:** `ceph-bluestore-tool` is crucial for diagnosing and repairing OSDs suffering from data corruption or issues with BlueStore’s internal data structures.
  
2. **RocksDB Issues:** The tool provides subcommands like `rebuild-db` and `compact` to manage the RocksDB used by BlueStore, which stores the object metadata. It can help resolve RocksDB corruption or performance degradation.

3. **Label and Metadata Management:** This tool can display important metadata about OSDs, such as the OSD ID, UUID, and other details stored in the label. It's useful for administrators managing multiple OSDs.

4. **Inspecting Object Store:** With commands like `list-objects`, Ceph administrators can inspect the contents of the BlueStore object store and take actions based on the data.

5. **Filesystem Integrity:** `ceph-bluestore-tool` helps ensure the integrity of the BlueStore filesystem and its associated databases, preventing or mitigating data loss scenarios.



## Conclusion

The `ceph-bluestore-tool` is essential for managing the integrity and performance of BlueStore OSDs in a Ceph cluster. It provides robust commands for diagnosing, repairing, and inspecting BlueStore’s storage and metadata, making it a critical utility for Ceph administrators responsible for cluster maintenance and troubleshooting.
