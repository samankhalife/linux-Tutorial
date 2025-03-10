# Ceph
Ceph is a powerful, scalable, and highly resilient distributed storage platform that can provide object, block, and file storage under a unified system. It consists of various daemons such as Monitors (MONs), Object Storage Daemons (OSDs), and Metadata Servers (MDS) for CephFS. Ceph's primary interface for interacting with the system is the `ceph` command-line tool, which provides various subcommands to manage, monitor, and troubleshoot the Ceph cluster.

Below is a detailed guide on the most commonly used `ceph` subcommands and their purposes.

## General Structure of `ceph` Command

```bash
ceph [options] <subcommand> [arguments]
```

- **`[options]`**: Flags such as `--admin-daemon`, `--cluster`, `-s` for status, etc.
- **`<subcommand>`**: The specific operation or management action you wish to perform (e.g., `status`, `health`, `osd`, `monitor`).
- **`[arguments]`**: Additional arguments required by the subcommand.


## Common `ceph` Subcommands

### 1. **Cluster Information and Status**

#### **`ceph status` (or `ceph -s`)**
Displays the overall health and status of the Ceph cluster. This command is frequently used for monitoring purposes.

```bash
ceph status
```

- Example Output:
  ```
  cluster:
    id:     e4a89f8c-4a64-4df5-bcdf-e246b6f8120e
    health: HEALTH_OK

  services:
    mon: 3 daemons, quorum mon1,mon2,mon3
    mgr: mgr1(active), mgr2(standby)
    osd: 20 osds: 20 up, 20 in
    mds: cephfs-1/1/1 up {0=mds1=up:active}, 1 up:standby
  ```

#### **`ceph health`**
Returns a concise health report for the cluster. This can be combined with additional options to filter warnings or errors.

```bash
ceph health
```

- Example Output:
  ```
  HEALTH_OK
  ```

Options:
- `ceph health detail` – Provides a more detailed health report with issues or warnings.

### 2. **Monitor Commands**

#### **`ceph mon dump`**
Displays the list of monitors, their ranks, and their addresses.

```bash
ceph mon dump
```

#### **`ceph quorum_status`**
Provides information about the quorum of the monitor nodes.

```bash
ceph quorum_status
```

#### **`ceph mon stat`**
Shows the status of the monitor nodes.

```bash
ceph mon stat
```

### 3. **OSD Commands**

#### **`ceph osd status`**
Provides a list of the Object Storage Daemons (OSDs) in the cluster and their statuses (e.g., up, down, in, out).

```bash
ceph osd status
```

#### **`ceph osd tree`**
Displays the OSDs organized in a hierarchical tree, often including information about the CRUSH hierarchy.

```bash
ceph osd tree
```

#### **`ceph osd df`**
Displays a detailed breakdown of disk usage and available space across OSDs in the cluster.

```bash
ceph osd df
```

#### **`ceph osd pool create`**
Creates a new pool within the Ceph cluster. A pool is a logical group of objects that can have its own replication settings.

```bash
ceph osd pool create <pool-name> <pg-num>
```

Example:
```bash
ceph osd pool create mypool 128
```

#### **`ceph osd pool delete`**
Deletes a pool from the cluster. **Be cautious** with this command, as it permanently deletes data.

```bash
ceph osd pool delete <pool-name> <pool-name> --yes-i-really-really-mean-it
```

#### **`ceph osd crush rule list`**
Lists the CRUSH (Controlled Replication Under Scalable Hashing) rules used for data placement in the cluster.

```bash
ceph osd crush rule list
```

#### **`ceph osd reweight`**
Adjusts the weight of an OSD to rebalance data across the cluster.

```bash
ceph osd reweight <osd-id> <weight>
```

Example:
```bash
ceph osd reweight osd.1 0.8
```

#### **`ceph osd out`**
Marks an OSD as "out" of the cluster, which stops data from being written to that OSD.

```bash
ceph osd out <osd-id>
```

#### **`ceph osd in`**
Marks an OSD as "in" the cluster, allowing it to receive data again.

```bash
ceph osd in <osd-id>
```

### 4. **Pool Commands**

#### **`ceph osd pool ls`**
Lists all pools in the cluster.

```bash
ceph osd pool ls
```

#### **`ceph osd pool set`**
Sets or modifies parameters of a given pool.

```bash
ceph osd pool set <pool-name> <option> <value>
```

Example (adjusting replication size):
```bash
ceph osd pool set mypool size 3
```

#### **`ceph osd pool get`**
Gets the value of a particular option for a given pool.

```bash
ceph osd pool get <pool-name> <option>
```

Example (getting the replication size):
```bash
ceph osd pool get mypool size
```

### 5. **MDS and CephFS Commands**

#### **`ceph fs status`**
Displays the status of CephFS (Ceph File System).

```bash
ceph fs status
```

#### **`ceph mds stat`**
Shows the status of all metadata servers (MDS) in the cluster.

```bash
ceph mds stat
```

#### **`ceph fs ls`**
Lists all CephFS file systems in the cluster.

```bash
ceph fs ls
```

#### **`ceph fs new`**
Creates a new CephFS file system.

```bash
ceph fs new <fs-name> <metadata-pool> <data-pool>
```

### 6. **Client and Admin Commands**

#### **`ceph config dump`**
Displays the current configuration for all Ceph components.

```bash
ceph config dump
```

#### **`ceph log`**
Displays logs for the Ceph cluster.

```bash
ceph log [daemon] <loglevel>
```

Example (viewing logs of the monitor service):
```bash
ceph log mon
```

### 7. **RBD (RADOS Block Device) Commands**

#### **`rbd ls`**
Lists all RADOS block devices in the cluster.

```bash
rbd ls
```

#### **`rbd create`**
Creates a new RADOS block device.

```bash
rbd create <image-name> --size <size>
```

Example:
```bash
rbd create mydisk --size 10G
```

#### **`rbd rm`**
Removes an existing RBD image.

```bash
rbd rm <image-name>
```

#### **`rbd map`**
Maps a RBD device to a local kernel module, making it available to be mounted as a block device on the system.

```bash
rbd map <image-name>
```

#### **`rbd unmap`**
Unmaps a previously mapped RBD device.

```bash
rbd unmap <image-name>
```

### 8. **Administrative Commands**

#### **`ceph auth list`**
Lists all authorization keys and capabilities in the cluster.

```bash
ceph auth list
```

#### **`ceph auth add`**
Adds a new authorization key with specified capabilities.

```bash
ceph auth add <entity> <caps>
```

Example:
```bash
ceph auth add client.admin mon 'allow *' osd 'allow *' mds 'allow'
```

#### **`ceph mgr module enable`**
Enables a manager module in Ceph. Ceph Manager (Mgr) modules offer additional services to the cluster.

```bash
ceph mgr module enable <module-name>
```

Example:
```bash
ceph mgr module enable dashboard
```

## Conclusion

The `ceph` command-line tool is highly versatile and allows administrators to control every aspect of a Ceph cluster. Whether it's managing OSDs, monitoring cluster health, configuring pools, or setting up RBD devices, `ceph` provides robust commands to handle these tasks efficiently.

For daily monitoring and administration, commands like `ceph status`, `ceph osd tree`, and `ceph osd df` provide essential insights into cluster performance, health, and resource utilization.
