# ceph-deploy
`ceph-deploy` is a deployment tool for Ceph, which is an open-source distributed storage system designed for high performance, scalability, and fault tolerance. The `ceph-deploy` tool simplifies the process of deploying and configuring Ceph clusters. It is primarily used for initial cluster setup, deployment of monitor nodes, OSDs (Object Storage Daemons), and other Ceph services.

Below is a summary of `ceph-deploy` and its most common subcommands.

## Overview of `ceph-deploy`

`ceph-deploy` is a simple command-line tool that automates much of the process involved in setting up and managing a Ceph cluster. It is intended for use in smaller environments or in situations where a minimal and straightforward deployment is needed. It is generally less flexible and robust than using other tools like `cephadm` or manually configuring Ceph, but it offers an easy path to quickly deploy a cluster.

### Basic Syntax

```bash
ceph-deploy [OPTIONS] <COMMAND> [ARGUMENTS]
```

Where:
- **<COMMAND>**: The specific action to be performed (e.g., `new`, `install`, `admin`).
- **[ARGUMENTS]**: Additional arguments relevant to the command.

## Common Subcommands for `ceph-deploy`

### 1. **ceph-deploy new**
Creates a new Ceph cluster by initializing the monitor and the OSDs.

```bash
ceph-deploy new <monitor_node> [<additional_monitor_nodes>...]
```

- **<monitor_node>**: The initial node that will serve as the Ceph monitor.
- **[additional_monitor_nodes]**: Optional additional monitor nodes to be included in the cluster.

#### Example:

```bash
ceph-deploy new mon1 mon2 mon3
```

This command initializes a Ceph cluster with three monitor nodes: `mon1`, `mon2`, and `mon3`.

### 2. **ceph-deploy install**
Installs Ceph on the specified nodes. This command installs Ceph packages on all the specified nodes and prepares them for deployment.

```bash
ceph-deploy install <node1> <node2> ...
```

- **<node1> <node2> ...**: The list of nodes where Ceph will be installed.

#### Example:

```bash
ceph-deploy install mon1 osd1 osd2 osd3
```

This command installs Ceph on `mon1`, `osd1`, `osd2`, and `osd3` nodes.

### 3. **ceph-deploy admin**
Copies the Ceph configuration files and admin keyrings to the specified node(s), enabling them to interact with the cluster.

```bash
ceph-deploy admin <node1> <node2> ...
```

- **<node1> <node2> ...**: Nodes where the admin configuration should be copied.

#### Example:

```bash
ceph-deploy admin mon1 osd1 osd2
```

This command copies the admin configuration to `mon1`, `osd1`, and `osd2`.

### 4. **ceph-deploy mon create-initial**
Creates the initial Ceph monitor and initializes the cluster. It’s used after `ceph-deploy new` to create the initial monitor.

```bash
ceph-deploy mon create-initial
```

This command creates the initial monitor after the cluster configuration is set up using `ceph-deploy new`.

#### Example:

```bash
ceph-deploy mon create-initial
```

This initializes the first monitor for the cluster.

### 5. **ceph-deploy osd create**
Creates an OSD (Object Storage Daemon) on a specified node. OSDs store the data, handle replication, and provide recovery in case of failure.

```bash
ceph-deploy osd create <node> --data <path_to_data_dir>
```

- **<node>**: The node where the OSD will be created.
- **--data <path_to_data_dir>**: Specifies the directory to be used for OSD data storage.

#### Example:

```bash
ceph-deploy osd create osd1 --data /dev/sdb
```

This command creates an OSD on `osd1` using the device `/dev/sdb`.

### 6. **ceph-deploy gatherkeys**
Gathers all of the necessary Ceph keys from the cluster and stores them on the local machine for administrative use.

```bash
ceph-deploy gatherkeys <node>
```

- **<node>**: The node from which the keys should be gathered.

#### Example:

```bash
ceph-deploy gatherkeys mon1
```

This command gathers the Ceph keys from the `mon1` node.

### 7. **ceph-deploy disk list**
Lists the available disks on a specified node, helping you determine which disks can be used for creating OSDs.

```bash
ceph-deploy disk list <node>
```

- **<node>**: The node where you want to list available disks.

#### Example:

```bash
ceph-deploy disk list osd1
```

This command lists the available disks on the `osd1` node.

### 8. **ceph-deploy disk zap**
Prepares a disk for use as an OSD by clearing it. This is required before creating an OSD on a new disk.

```bash
ceph-deploy disk zap <node> <disk>
```

- **<node>**: The node where the disk is located.
- **<disk>**: The disk to be cleared (zapped).

#### Example:

```bash
ceph-deploy disk zap osd1 /dev/sdb
```

This command zaps the `/dev/sdb` disk on `osd1`, preparing it for use as an OSD.

### 9. **ceph-deploy mon destroy**
Destroys a monitor on a specified node. This is used when you need to remove a monitor from the cluster.

```bash
ceph-deploy mon destroy <node>
```

- **<node>**: The node where the monitor should be destroyed.

#### Example:

```bash
ceph-deploy mon destroy mon1
```

This command destroys the monitor on the `mon1` node.

### 10. **ceph-deploy osd destroy**
Destroys an OSD on a specified node. This is used when you need to remove an OSD from the cluster.

```bash
ceph-deploy osd destroy <node> --data <path_to_data_dir>
```

- **<node>**: The node where the OSD should be destroyed.
- **--data <path_to_data_dir>**: Specifies the directory or device used by the OSD.

#### Example:

```bash
ceph-deploy osd destroy osd1 --data /dev/sdb
```

This command destroys the OSD on `osd1` that used `/dev/sdb`.

### 11. **ceph-deploy mon add**
Adds additional monitors to an existing Ceph cluster.

```bash
ceph-deploy mon add <node>
```

- **<node>**: The node to which the monitor should be added.

#### Example:

```bash
ceph-deploy mon add mon4
```

This command adds a new monitor (`mon4`) to the existing cluster.

## Example Workflow for Deploying Ceph with `ceph-deploy`

1. **Create a new Ceph cluster**:
   ```bash
   ceph-deploy new mon1
   ```

2. **Install Ceph on nodes**:
   ```bash
   ceph-deploy install mon1 osd1 osd2
   ```

3. **Copy the admin keys to all nodes**:
   ```bash
   ceph-deploy admin mon1 osd1 osd2
   ```

4. **Create initial monitor**:
   ```bash
   ceph-deploy mon create-initial
   ```

5. **Create OSDs on the nodes**:
   ```bash
   ceph-deploy osd create osd1 --data /dev/sdb
   ceph-deploy osd create osd2 --data /dev/sdc
   ```

6. **Gather the keys**:
   ```bash
   ceph-deploy gatherkeys mon1
   ```

7. **Check cluster status**:
   ```bash
   ceph -s
   ```

## Conclusion

`ceph-deploy` is a great tool for deploying and managing Ceph clusters, especially in smaller environments or for proof of concepts. It simplifies much of the work involved in setting up a Ceph cluster, from installing packages to creating monitors and OSDs. However, for larger or more complex environments, you might want to consider using tools like `cephadm` or manually configuring Ceph, as `ceph-deploy` is less flexible and doesn't offer the same level of customization for more advanced use cases.
