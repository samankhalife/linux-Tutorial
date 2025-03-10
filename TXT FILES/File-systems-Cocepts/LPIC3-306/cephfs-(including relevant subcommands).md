# CephFS
CephFS (Ceph Filesystem) is a distributed file system that provides high-performance, scalable, and fault-tolerant file storage on top of a Ceph cluster. The `cephfs` tool allows for the management of a CephFS instance, and many operations are performed using Ceph administrative tools like `ceph`, `mount`, `rados`, and other filesystem tools. However, there are specific subcommands and operations associated with managing CephFS.

Below is a breakdown of `cephfs`-related subcommands and relevant operations for managing the Ceph filesystem:



## General Structure of CephFS Commands

### Using the `ceph` CLI to manage CephFS:
```bash
ceph fs <subcommand> [options]
```



## Common `cephfs` Subcommands

### 1. **Filesystem Management**

#### **`ceph fs create`**
Creates a new Ceph filesystem (CephFS) instance.

```bash
ceph fs create <filesystem-name> <metadata-pool> <data-pool>
```

- Example:
  ```bash
  ceph fs create myfs cephfs_metadata cephfs_data
  ```

This creates a new CephFS instance named `myfs`, with `cephfs_metadata` as the metadata pool and `cephfs_data` as the data pool.

#### **`ceph fs ls`**
Lists all the CephFS filesystems available in the Ceph cluster.

```bash
ceph fs ls
```

- Example:
  ```bash
  ceph fs ls
  ```

This lists all the filesystems configured in the Ceph cluster.

#### **`ceph fs rm`**
Removes a CephFS filesystem from the cluster.

```bash
ceph fs rm <filesystem-name> --yes-i-really-mean-it
```

- Example:
  ```bash
  ceph fs rm myfs --yes-i-really-mean-it
  ```

This removes the filesystem `myfs` from the cluster (use with caution).



### 2. **MDS (Metadata Server) Management**

#### **`ceph fs status`**
Displays detailed status information about a CephFS instance, including MDS activity.

```bash
ceph fs status [<filesystem-name>]
```

- Example:
  ```bash
  ceph fs status myfs
  ```

This shows the status of the filesystem `myfs`, including the MDS status and client connections.

#### **`ceph fs set`**
Sets various configuration options for a specific CephFS filesystem.

```bash
ceph fs set <filesystem-name> <option> <value>
```

- Example:
  ```bash
  ceph fs set myfs max_mds 2
  ```

This sets the maximum number of MDS daemons for the filesystem `myfs` to 2.

#### **`ceph fs dump`**
Dumps the full configuration of a CephFS instance, including metadata pool, data pool, MDS settings, and placement groups.

```bash
ceph fs dump
```

- Example:
  ```bash
  ceph fs dump
  ```

This provides a detailed output of the configuration and status of the CephFS instances.

#### **`ceph fs mds fail`**
Manually forces a failover of an MDS daemon to test failover functionality or to replace a non-responsive MDS.

```bash
ceph fs mds fail <rank>
```

- Example:
  ```bash
  ceph fs mds fail 0
  ```

This forces the failover of the MDS daemon with rank 0.

#### **`ceph fs mds stop`**
Stops a specific MDS daemon.

```bash
ceph fs mds stop <rank>
```

- Example:
  ```bash
  ceph fs mds stop 0
  ```

This stops the MDS daemon with rank 0.



### 3. **Snapshot Management**

#### **`ceph fs snap create`**
Creates a snapshot of a CephFS directory.

```bash
ceph fs snap create <filesystem-name> <path>@<snapshot-name>
```

- Example:
  ```bash
  ceph fs snap create myfs /@mysnap
  ```

This creates a snapshot `mysnap` of the root directory `/` in the filesystem `myfs`.

#### **`ceph fs snap ls`**
Lists all snapshots for a specified CephFS directory.

```bash
ceph fs snap ls <filesystem-name> <path>
```

- Example:
  ```bash
  ceph fs snap ls myfs /
  ```

This lists all snapshots in the root directory `/` of the `myfs` filesystem.

#### **`ceph fs snap rm`**
Removes a specific snapshot from a CephFS directory.

```bash
ceph fs snap rm <filesystem-name> <path>@<snapshot-name>
```

- Example:
  ```bash
  ceph fs snap rm myfs /@mysnap
  ```

This removes the snapshot `mysnap` from the root directory `/` in the `myfs` filesystem.



### 4. **Quota Management**

#### **`ceph fs set-quota`**
Sets a quota on a specified directory in a CephFS filesystem.

```bash
ceph fs set-quota <filesystem-name> <path> [max_bytes <bytes>] [max_files <count>]
```

- Example:
  ```bash
  ceph fs set-quota myfs /mydir max_bytes 104857600
  ```

This sets a 100MB quota on the directory `/mydir` in the filesystem `myfs`.

#### **`ceph fs get-quota`**
Retrieves the current quota settings for a specified directory in a CephFS filesystem.

```bash
ceph fs get-quota <filesystem-name> <path>
```

- Example:
  ```bash
  ceph fs get-quota myfs /mydir
  ```

This retrieves the quota settings for the directory `/mydir` in the filesystem `myfs`.



### 5. **Client Management**

#### **`ceph fs authorize`**
Authorizes a Ceph client to access a specific CephFS filesystem with read, write, or full permissions.

```bash
ceph fs authorize <filesystem-name> <client-id> <caps>
```

- Example:
  ```bash
  ceph fs authorize myfs client.myclient rw
  ```

This authorizes the client `client.myclient` to have read/write access to the `myfs` filesystem.

#### **`ceph fs deauthorize`**
Revokes a Ceph client’s access to a specified filesystem.

```bash
ceph fs deauthorize <filesystem-name> <client-id>
```

- Example:
  ```bash
  ceph fs deauthorize myfs client.myclient
  ```

This revokes the client `client.myclient`'s access to the `myfs` filesystem.



### 6. **Mounting a CephFS Filesystem**

#### **Mount via Kernel Client**
You can mount a CephFS using the Linux kernel client.

```bash
mount -t ceph <mon-address>:<mon-port>,<mon-address>:<mon-port>:/ /mnt/mycephfs -o name=<client-name>,secretfile=<path-to-secret>
```

- Example:
  ```bash
  mount -t ceph 10.0.0.1:6789:/ /mnt/mycephfs -o name=admin,secretfile=/etc/ceph/ceph.client.admin.keyring
  ```

This mounts the CephFS root `/` to the `/mnt/mycephfs` directory, using the admin keyring for authentication.

#### **Mount via FUSE**
You can also mount CephFS using the FUSE client.

```bash
ceph-fuse /mnt/mycephfs --client_mds_namespace=<filesystem-name> -m <mon-address>
```

- Example:
  ```bash
  ceph-fuse /mnt/mycephfs --client_mds_namespace=myfs -m 10.0.0.1
  ```

This mounts the CephFS filesystem `myfs` to `/mnt/mycephfs` using the FUSE client.


### 7. **Pool Management**

#### **`ceph fs add_data_pool`**
Adds a new data pool to an existing CephFS filesystem.

```bash
ceph fs add_data_pool <filesystem-name> <data-pool>
```

- Example:
  ```bash
  ceph fs add_data_pool myfs cephfs_data2
  ```

This adds a new data pool `cephfs_data2` to the filesystem `myfs`.

#### **`ceph fs set default_pool`**
Sets a pool as the default data or metadata pool for a CephFS filesystem.

```bash
ceph fs set <filesystem-name> <pool-type> <pool-name>
```

- Example:
  ```bash
  ceph fs set myfs data_pool cephfs_data2
  ```

This sets `cephfs_data2` as the default data pool for the filesystem `myfs`.

## Conclusion

CephFS offers rich functionality for managing distributed filesystems within a Ceph cluster. From creating filesystems and managing MDS daemons to handling quotas, snapshots, and client permissions, the `ceph fs` suite of commands provides the necessary tools to administer CephFS instances effectively. Additionally, CephFS integrates with Ceph’s powerful object store, making it a flexible solution for large-scale, high-performance storage environments
