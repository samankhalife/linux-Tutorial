# ceph-volume
`ceph-volume` is a Ceph tool used to manage and provision OSDs (Object Storage Daemons) on a Ceph cluster. It supports various types of storage backends (e.g., `lvm`, `raw`, `bluestore`, `filestore`) and provides functionality for creating, listing, and destroying OSDs. 

Here are the relevant subcommands and their common usage:



## Common `ceph-volume` Subcommands

### 1. **ceph-volume lvm**

The `ceph-volume lvm` subcommand is used to manage OSDs backed by LVM (Logical Volume Manager). Ceph OSDs are often deployed using `bluestore` or `filestore` on LVM partitions.

#### **`ceph-volume lvm create`**
Creates a new OSD backed by LVM.

```bash
ceph-volume lvm create --data <device>
```

- Example:
  ```bash
  ceph-volume lvm create --data /dev/sdb
  ```

This command creates a new OSD on the device `/dev/sdb`. By default, it creates a `bluestore` OSD, but you can specify `filestore` if needed:

- Example for `filestore`:
  ```bash
  ceph-volume lvm create --filestore --data /dev/sdb
  ```

#### **`ceph-volume lvm list`**
Lists all OSDs that are backed by LVM.

```bash
ceph-volume lvm list
```

- Example:
  ```bash
  ceph-volume lvm list
  ```

This displays detailed information about all LVM-backed OSDs in the system.

#### **`ceph-volume lvm zap`**
Destroys the contents of a device (zaps) to prepare it for reuse.

```bash
ceph-volume lvm zap <device>
```

- Example:
  ```bash
  ceph-volume lvm zap /dev/sdb
  ```

This wipes all data and partitioning information from the device `/dev/sdb`, making it ready for new OSD creation.

#### **`ceph-volume lvm activate`**
Activates an existing OSD by associating it with the Ceph cluster.

```bash
ceph-volume lvm activate --all
```

- Example:
  ```bash
  ceph-volume lvm activate --all
  ```

This activates all LVM-backed OSDs in the system, making them part of the running Ceph cluster.



### 2. **ceph-volume raw**

The `ceph-volume raw` subcommand is used to manage OSDs without LVM, particularly for `bluestore` OSDs that don't require LVM as a backend.

#### **`ceph-volume raw create`**
Creates a new OSD without LVM.

```bash
ceph-volume raw create --data <device>
```

- Example:
  ```bash
  ceph-volume raw create --data /dev/sdc
  ```

This creates a `bluestore` OSD on the raw device `/dev/sdc` without using LVM.

#### **`ceph-volume raw list`**
Lists all OSDs that are not backed by LVM (raw OSDs).

```bash
ceph-volume raw list
```

- Example:
  ```bash
  ceph-volume raw list
  ```

This displays detailed information about all raw OSDs in the system.

#### **`ceph-volume raw zap`**
Zaps (wipes) a raw device to prepare it for reuse.

```bash
ceph-volume raw zap <device>
```

- Example:
  ```bash
  ceph-volume raw zap /dev/sdc
  ```

This wipes all data and partitioning information from the raw device `/dev/sdc`, preparing it for reuse.



### 3. **ceph-volume simple**

The `ceph-volume simple` subcommand is a legacy command used to manage OSDs before `lvm` and `raw` methods were introduced. It's now deprecated but still supported for backward compatibility.

#### **`ceph-volume simple scan`**
Scans a device to gather information about existing OSDs.

```bash
ceph-volume simple scan <device>
```

- Example:
  ```bash
  ceph-volume simple scan /dev/sdd
  ```

This scans the device `/dev/sdd` to check if an OSD is already present or if it can be reused.

#### **`ceph-volume simple activate`**
Activates an existing OSD using the legacy `simple` method.

```bash
ceph-volume simple activate --all
```

- Example:
  ```bash
  ceph-volume simple activate --all
  ```

This activates all OSDs managed by the `simple` backend.



### 4. **ceph-volume inventory**

The `ceph-volume inventory` subcommand is used to display the inventory of available devices that can be used for OSD creation.

#### **`ceph-volume inventory`**
Lists all available devices on the host that can be used for OSD creation, showing if they are zapped, have partitions, or contain OSDs.

```bash
ceph-volume inventory
```

- Example:
  ```bash
  ceph-volume inventory
  ```

This command provides detailed information about all devices available for OSD use on the system, indicating their status.



### 5. **ceph-volume trigger**

The `ceph-volume trigger` subcommand allows manual triggering of specific events for OSDs, such as triggering a rescan of LVM devices.

#### **`ceph-volume trigger rescan`**
Triggers a rescan of LVM devices to ensure that all OSDs are properly detected and activated.

```bash
ceph-volume trigger rescan
```

- Example:
  ```bash
  ceph-volume trigger rescan
  ```

This forces a rescan of LVM devices, ensuring that the cluster has up-to-date information on all OSDs.



### 6. **ceph-volume systemd**

The `ceph-volume systemd` subcommand helps manage the interaction between OSDs and systemd units for service management.

#### **`ceph-volume systemd list`**
Lists all the systemd unit files related to OSDs.

```bash
ceph-volume systemd list
```

- Example:
  ```bash
  ceph-volume systemd list
  ```

This command displays all the systemd units managing OSDs, showing their statuses.

#### **`ceph-volume systemd activate`**
Activates systemd unit files for OSDs.

```bash
ceph-volume systemd activate --all
```

- Example:
  ```bash
  ceph-volume systemd activate --all
  ```

This activates all the systemd unit files responsible for managing the OSDs.



## Conclusion

The `ceph-volume` tool is essential for managing the lifecycle of Ceph OSDs, offering flexibility in choosing between LVM and raw devices. Its subcommands allow you to create, list, activate, and zap OSDs, and manage the inventory of available devices. By providing options for both legacy and modern methods of OSD provisioning, `ceph-volume` ensures the robust and efficient management of Ceph storage resources.
