# rados
The `rados` command-line tool is used to interact directly with the underlying RADOS (Reliable Autonomic Distributed Object Store) in Ceph. This tool allows for performing low-level operations on RADOS objects, pools, and monitors, such as creating, reading, writing, and listing objects in pools. 

Here’s a detailed guide to the most common `rados` subcommands and their purposes:

## General Structure of `rados` Command

```bash
rados [options] <subcommand> [arguments]
```

- **`[options]`**: Global options such as `--pool`, `--cluster`, etc.
- **`<subcommand>`**: The specific operation or management action to be performed (e.g., `ls`, `get`, `put`, `rm`).
- **`[arguments]`**: Additional arguments required by the subcommand.

## Common `rados` Subcommands

### 1. **Object Manipulation**

These commands allow you to manipulate individual objects in RADOS pools.

#### **`rados put`**
Writes data from a file or standard input to a RADOS object in a specified pool.

```bash
rados --pool <pool-name> put <object-name> <file-name>
```

- Example:
  ```bash
  rados --pool mypool put object1 file.txt
  ```

This writes the contents of `file.txt` into an object named `object1` in the `mypool` pool.

#### **`rados get`**
Retrieves data from a RADOS object and saves it to a file or prints it to standard output.

```bash
rados --pool <pool-name> get <object-name> <file-name>
```

- Example:
  ```bash
  rados --pool mypool get object1 retrieved.txt
  ```

This retrieves the contents of the object `object1` from the `mypool` pool and saves it to `retrieved.txt`.

#### **`rados rm`**
Removes a RADOS object from a specified pool.

```bash
rados --pool <pool-name> rm <object-name>
```

- Example:
  ```bash
  rados --pool mypool rm object1
  ```

This deletes the object `object1` from the `mypool` pool.

### 2. **Object Listing and Information**

#### **`rados ls`**
Lists all objects in a specified pool.

```bash
rados --pool <pool-name> ls
```

- Example:
  ```bash
  rados --pool mypool ls
  ```

This will list all objects in the `mypool` pool.

#### **`rados stat`**
Displays metadata for a specific object, such as size, timestamps, and location.

```bash
rados --pool <pool-name> stat <object-name>
```

- Example:
  ```bash
  rados --pool mypool stat object1
  ```

This shows statistics about the object `object1` in the `mypool` pool.

### 3. **Object Operations**

#### **`rados append`**
Appends data to an existing RADOS object.

```bash
rados --pool <pool-name> append <object-name> <file-name>
```

- Example:
  ```bash
  rados --pool mypool append object1 additional_data.txt
  ```

This appends the contents of `additional_data.txt` to the object `object1` in the `mypool` pool.

#### **`rados write`**
Writes data to a RADOS object from a file but allows more granular control (e.g., specifying offsets).

```bash
rados --pool <pool-name> write <object-name> <file-name> [offset]
```

- Example:
  ```bash
  rados --pool mypool write object1 data.txt 1024
  ```

This writes the contents of `data.txt` to the object `object1` at an offset of 1024 bytes.

---

### 4. **Pool Management**

#### **`rados df`**
Displays disk usage and object statistics for a RADOS pool or for all pools.

```bash
rados df
```

This shows disk usage and object distribution across all pools in the cluster.

#### **`rados pool create`**
Creates a new RADOS pool.

```bash
rados mkpool <pool-name>
```

- Example:
  ```bash
  rados mkpool mypool
  ```

This creates a new pool named `mypool`.

#### **`rados pool delete`**
Deletes an existing RADOS pool. **Be cautious** when using this command, as it permanently removes all data in the pool.

```bash
rados rmpool <pool-name> <pool-name> --yes-i-really-really-mean-it
```

- Example:
  ```bash
  rados rmpool mypool mypool --yes-i-really-really-mean-it
  ```

This deletes the pool named `mypool`.

#### **`rados pool ls`**
Lists all pools in the cluster.

```bash
rados pool ls
```

This command lists all the pools available in the Ceph cluster.


### 5. **Monitoring and Statistics**

#### **`rados bench`**
Performs a benchmarking test on a specific pool by writing or reading objects of a given size for a specified duration.

```bash
rados --pool <pool-name> bench <seconds> <operation>
```

- Example:
  ```bash
  rados --pool mypool bench 10 write
  ```

This performs a write benchmark test for 10 seconds on the pool `mypool`.

#### **`rados ping`**
Pings a specific monitor or OSD to verify its health and connectivity.

```bash
rados ping <target>
```

- Example:
  ```bash
  rados ping mon.a
  ```

This pings the monitor with the ID `mon.a`.

#### **`rados stat`**
Displays statistics and metadata about a specific RADOS object.

```bash
rados --pool <pool-name> stat <object-name>
```

- Example:
  ```bash
  rados --pool mypool stat object1
  ```

This displays detailed information about the object `object1` in the pool `mypool`.

### 6. **Snapshots and Cloning**

#### **`rados mksnap`**
Creates a snapshot of a pool.

```bash
rados mksnap <pool-name> <snapshot-name>
```

- Example:
  ```bash
  rados mksnap mypool mysnapshot
  ```

This creates a snapshot of the `mypool` pool named `mysnapshot`.

#### **`rados rmsnap`**
Removes a snapshot from a pool.

```bash
rados rmsnap <pool-name> <snapshot-name>
```

- Example:
  ```bash
  rados rmsnap mypool mysnapshot
  ```

This removes the snapshot `mysnapshot` from the `mypool` pool.

#### **`rados clone`**
Creates a copy (clone) of an existing object within a RADOS pool.

```bash
rados --pool <pool-name> clone <original-object> <clone-object>
```

- Example:
  ```bash
  rados --pool mypool clone object1 object1_clone
  ```

This clones the object `object1` into a new object `object1_clone` within the `mypool` pool.

### 7. **Replication and Data Placement**

#### **`rados setomapval`**
Sets an Object Map (omap) key-value pair on an object in a pool.

```bash
rados --pool <pool-name> setomapval <object-name> <key> <value>
```

- Example:
  ```bash
  rados --pool mypool setomapval object1 mykey myvalue
  ```

This sets an omap key-value pair `mykey=myvalue` on the object `object1` in the pool `mypool`.

#### **`rados getomapval`**
Retrieves a specific key-value pair from the omap of an object.

```bash
rados --pool <pool-name> getomapval <object-name> <key>
```

- Example:
  ```bash
  rados --pool mypool getomapval object1 mykey
  ```

This retrieves the value of the omap key `mykey` from the object `object1` in the pool `mypool`.

## Conclusion

The `rados` tool provides powerful and fine-grained control over individual objects and pools in the Ceph RADOS storage system. Whether it’s performing object I/O operations, managing pools, or monitoring cluster health and performance, `rados` allows direct interaction with the object store, making it essential for system administrators managing large Ceph storage clusters.

By mastering these commands, you can efficiently manage Ceph’s underlying object store, perform diagnostics, and optimize storage.
