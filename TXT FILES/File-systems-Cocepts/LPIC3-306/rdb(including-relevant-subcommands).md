# rbd
The `rbd` (RADOS Block Device) command-line tool is used to manage block devices in a Ceph storage cluster. RADOS Block Devices (RBD) are block storage volumes backed by the Ceph distributed object store. These can be used for cloud infrastructure, virtual machines, or other applications that need block storage.

Here’s a detailed overview of common `rbd` subcommands and their usage:



## General Structure of `rbd` Command

```bash
rbd [options] <subcommand> [arguments]
```

- **`[options]`**: Global options such as `--pool`, `--cluster`, etc.
- **`<subcommand>`**: The specific operation or management action to be performed (e.g., `create`, `info`, `rm`).
- **`[arguments]`**: Additional arguments required by the subcommand.



## Common `rbd` Subcommands

### 1. **Image Management**

#### **`rbd create`**
Creates a new RADOS Block Device (RBD) image.

```bash
rbd create <image-name> --size <size-in-MB|GB|TB> [options]
```

- Example:
  ```bash
  rbd create myimage --size 10G
  ```

This creates a new image named `myimage` of size 10 GB.

#### **`rbd rm`**
Removes a specified RBD image from a pool.

```bash
rbd rm <image-name> [--pool <pool-name>]
```

- Example:
  ```bash
  rbd rm myimage
  ```

This deletes the image `myimage` from the pool.

#### **`rbd info`**
Displays information about an RBD image, such as size, object size, features, etc.

```bash
rbd info <image-name>
```

- Example:
  ```bash
  rbd info myimage
  ```

This shows detailed information about the image `myimage`.

#### **`rbd resize`**
Resizes an existing RBD image.

```bash
rbd resize --size <new-size> <image-name>
```

- Example:
  ```bash
  rbd resize --size 20G myimage
  ```

This resizes the `myimage` to 20 GB.



### 2. **Image Listing and Mapping**

#### **`rbd ls`**
Lists all RBD images in a specified pool.

```bash
rbd ls [--pool <pool-name>]
```

- Example:
  ```bash
  rbd ls
  ```

This lists all RBD images in the default pool or the specified pool.

#### **`rbd map`**
Maps an RBD image to a block device on the local system.

```bash
rbd map <image-name> [--pool <pool-name>]
```

- Example:
  ```bash
  rbd map myimage
  ```

This maps the image `myimage` to a block device (e.g., `/dev/rbd0`) on the local system.

#### **`rbd unmap`**
Unmaps an RBD image from the local system.

```bash
rbd unmap /dev/rbd<x>
```

- Example:
  ```bash
  rbd unmap /dev/rbd0
  ```

This unmaps the block device `/dev/rbd0`.



### 3. **Image Snapshot Management**

#### **`rbd snap create`**
Creates a snapshot of an RBD image.

```bash
rbd snap create <image-name>@<snapshot-name>
```

- Example:
  ```bash
  rbd snap create myimage@mysnap
  ```

This creates a snapshot `mysnap` of the image `myimage`.

#### **`rbd snap ls`**
Lists all snapshots for a given image.

```bash
rbd snap ls <image-name>
```

- Example:
  ```bash
  rbd snap ls myimage
  ```

This lists all snapshots of the image `myimage`.

#### **`rbd snap rollback`**
Rolls back an image to a specific snapshot.

```bash
rbd snap rollback <image-name>@<snapshot-name>
```

- Example:
  ```bash
  rbd snap rollback myimage@mysnap
  ```

This rolls back the image `myimage` to the snapshot `mysnap`.

#### **`rbd snap rm`**
Removes a specific snapshot.

```bash
rbd snap rm <image-name>@<snapshot-name>
```

- Example:
  ```bash
  rbd snap rm myimage@mysnap
  ```

This removes the snapshot `mysnap` from the image `myimage`.



### 4. **Image Cloning**

#### **`rbd clone`**
Clones an RBD image from a snapshot to create a new image.

```bash
rbd clone <parent-image>@<snapshot-name> <new-image-name>
```

- Example:
  ```bash
  rbd clone myimage@mysnap myimage-clone
  ```

This creates a new image `myimage-clone` as a clone of the snapshot `mysnap` from the image `myimage`.

### 5. **Layering and Caching**

#### **`rbd feature disable`**
Disables specific features (e.g., layering) on an RBD image.

```bash
rbd feature disable <image-name> <feature>
```

- Example:
  ```bash
  rbd feature disable myimage layering
  ```

This disables the `layering` feature for the image `myimage`.

#### **`rbd feature enable`**
Enables specific features (e.g., layering) on an RBD image.

```bash
rbd feature enable <image-name> <feature>
```

- Example:
  ```bash
  rbd feature enable myimage layering
  ```

This enables the `layering` feature for the image `myimage`.

### 6. **Export and Import**

#### **`rbd export`**
Exports an RBD image to a file.

```bash
rbd export <image-name> <file-name>
```

- Example:
  ```bash
  rbd export myimage myimage_export.raw
  ```

This exports the `myimage` to a file named `myimage_export.raw`.

#### **`rbd import`**
Imports an image from a file into an RBD image.

```bash
rbd import <file-name> <image-name>
```

- Example:
  ```bash
  rbd import myimage_export.raw myimage
  ```

This imports the image from `myimage_export.raw` and stores it as a new image `myimage` in the pool.

#### **`rbd import-diff`**
Applies incremental differences to an RBD image from a file (created by `rbd export-diff`).

```bash
rbd import-diff <file-name> <image-name>
```

- Example:
  ```bash
  rbd import-diff myimage_diff myimage
  ```

This applies incremental changes to the `myimage` from the file `myimage_diff`.

### 7. **Advanced Operations**

#### **`rbd lock add`**
Adds a lock to an image, which prevents other clients from modifying the image.

```bash
rbd lock add <image-name>
```

- Example:
  ```bash
  rbd lock add myimage
  ```

This adds a lock on the `myimage`, preventing modification by other clients.

#### **`rbd lock remove`**
Removes a lock from an image.

```bash
rbd lock remove <image-name> <lock-id> <locker-id>
```

- Example:
  ```bash
  rbd lock remove myimage lockid lockerid
  ```

This removes the lock on the `myimage` with the specific lock ID and locker ID.

#### **`rbd du`**
Displays disk usage information for a specific RBD image.

```bash
rbd du <image-name>
```

- Example:
  ```bash
  rbd du myimage
  ```

This shows how much space is being used by the `myimage`.

#### **`rbd bench`**
Performs a benchmark test on an RBD image.

```bash
rbd bench <image-name> [options]
```

- Example:
  ```bash
  rbd bench myimage --io-type write --io-size 4M --io-total 1024M
  ```

This performs a benchmark test with 4 MB write I/O operations on `myimage` for a total of 1024 MB.

## Conclusion

The `rbd` command provides extensive tools for managing block devices in Ceph, including creating, listing, resizing, and removing RBD images. You can also perform advanced operations like snapshots, cloning, exporting, and importing, as well as setting up features like layering. Mastering the `rbd` tool enables fine control over RADOS Block Devices, making it an essential skill for managing block storage in Ceph-based environments.
