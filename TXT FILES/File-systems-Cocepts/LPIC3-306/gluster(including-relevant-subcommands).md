# gluster

Gluster is an open-source distributed file system that enables you to scale storage across multiple machines, allowing for flexible storage management with a focus on high availability and fault tolerance. It is designed to handle large-scale data storage needs and provides high-performance storage with scalability and redundancy. Gluster uses a modular approach where volumes are distributed across several servers and can be accessed as a single file system.

The `gluster` command is the primary utility used for managing and configuring GlusterFS. This command allows administrators to manage clusters, create and manage volumes, check the status of the storage, and configure various aspects of the GlusterFS system.

## Purpose

- **Cluster Management**:  
  Allows administrators to create and manage Gluster clusters (groups of machines acting as one storage resource).
  
- **Volume Management**:  
  Enables the creation, modification, and deletion of Gluster volumes, which are logical units for storing data.

- **Storage Configuration**:  
  Configures storage options such as replication, striping, and distribution for high availability and fault tolerance.

- **Monitoring and Status**:  
  Provides commands to monitor the health, status, and performance of the Gluster system and its volumes.

## Basic Syntax

```bash
gluster [OPTIONS] <COMMAND> [ARGUMENTS]
```

Where:
- **<COMMAND>**: The specific Gluster operation to perform (e.g., creating a volume, managing clusters, etc.).
- **[ARGUMENTS]**: Additional options or parameters required for the command.

## Common Commands and Subcommands

### 1. **gluster volume create**

Used to create a Gluster volume, specifying the servers and directories to be used in the volume.

```bash
gluster volume create <volume_name> <transport> <hostname>:/path/to/brick [<hostname2>:/path/to/brick2]...
```

- **<volume_name>**: The name of the volume.
- **<transport>**: The transport type (e.g., `tcp`, `rdma`).
- **<hostname>:/path/to/brick**: Specifies the server and the path to the directory that will be part of the volume (called a "brick").

#### Example:

```bash
gluster volume create gv0 replica 2 transport tcp server1:/data/brick1 server2:/data/brick2
```

This command creates a replicated volume `gv0` with two bricks, one on `server1` and one on `server2`, using TCP transport.

### 2. **gluster volume start**

Starts the Gluster volume so it can be mounted and used.

```bash
gluster volume start <volume_name>
```

#### Example:

```bash
gluster volume start gv0
```

This command starts the volume `gv0`.

### 3. **gluster volume stop**

Stops a Gluster volume, effectively unmounting it and disabling access to it.

```bash
gluster volume stop <volume_name>
```

#### Example:

```bash
gluster volume stop gv0
```

This command stops the volume `gv0`.

### 4. **gluster volume info**

Displays detailed information about a specific volume, including its status, bricks, and configuration.

```bash
gluster volume info <volume_name>
```

#### Example:

```bash
gluster volume info gv0
```

This command provides information about the `gv0` volume, including its status and configuration.

### 5. **gluster volume status**

Shows the real-time status of the volume, including brick status and health.

```bash
gluster volume status <volume_name>
```

#### Example:

```bash
gluster volume status gv0
```

This command provides the status of `gv0`, including whether each brick is online or offline.

### 6. **gluster volume set**

Used to configure or change specific volume options such as performance tuning, replica counts, etc.

```bash
gluster volume set <volume_name> <option> <value>
```

#### Example:

```bash
gluster volume set gv0 performance.cache-size 1GB
```

This command sets the cache size to 1GB for the volume `gv0`.

### 7. **gluster volume remove-brick**

Removes a brick from an existing volume. This operation is useful for rebalancing a volume or removing a faulty server from the cluster.

```bash
gluster volume remove-brick <volume_name> <hostname>:/path/to/brick
```

#### Example:

```bash
gluster volume remove-brick gv0 server2:/data/brick2
```

This command removes the brick located on `server2` from the volume `gv0`.

### 8. **gluster volume rebalance**

Rebalances the distribution of data across the bricks of a volume, often used after adding or removing bricks.

```bash
gluster volume rebalance <volume_name> start
```

#### Example:

```bash
gluster volume rebalance gv0 start
```

This command starts the rebalance operation on the `gv0` volume.

### 9. **gluster volume heal**

Fixes split-brain scenarios by resolving inconsistencies between replicas in a volume.

```bash
gluster volume heal <volume_name> full
```

#### Example:

```bash
gluster volume heal gv0 full
```

This command heals the `gv0` volume by synchronizing data between replica bricks.

### 10. **gluster peer probe**

Adds a new peer (server) to the Gluster cluster.

```bash
gluster peer probe <hostname>
```

#### Example:

```bash
gluster peer probe server3
```

This command adds `server3` to the existing Gluster cluster.

### 11. **gluster peer status**

Displays the status of the Gluster peers (i.e., other servers in the cluster).

```bash
gluster peer status
```

#### Example:

```bash
gluster peer status
```

This command shows the status of all peers in the Gluster cluster.

### 12. **gluster volume reset**

Resets a specific volume’s options, essentially clearing all configuration changes made to the volume.

```bash
gluster volume reset <volume_name>
```

#### Example:

```bash
gluster volume reset gv0
```

This command resets the configuration for the `gv0` volume.

## Example Usage

1. **Creating a Distributed Volume**
   ```bash
   gluster volume create gv0 transport tcp server1:/data/brick1 server2:/data/brick2
   gluster volume start gv0
   ```

2. **Checking the Status of a Volume**
   ```bash
   gluster volume status gv0
   ```

3. **Adding a New Server to the Cluster**
   ```bash
   gluster peer probe server3
   ```

4. **Rebalancing a Volume**
   ```bash
   gluster volume rebalance gv0 start
   ```

5. **Removing a Brick from the Volume**
   ```bash
   gluster volume remove-brick gv0 server2:/data/brick2
   ```

## Best Practices

- **Monitor Volume Health Regularly**:  
  Ensure that the status of the volumes and the servers in the Gluster cluster are regularly checked to avoid performance issues.

- **Balance the Load Across Bricks**:  
  When adding new bricks to a volume, always perform a rebalance to ensure data is evenly distributed.

- **Use Replication for High Availability**:  
  Always create replicated volumes for fault tolerance, especially in production environments, to ensure data is not lost during server failures.

- **Test Recovery Procedures**:  
  Regularly test the ability to recover data from your Gluster volumes, including using the `heal` operation for split-brain scenarios.

## Conclusion

The `gluster` command is a powerful tool for managing and configuring GlusterFS, enabling administrators to create, modify, and monitor distributed storage volumes. With commands for volume creation, scaling, and data protection, GlusterFS provides a flexible and fault-tolerant storage solution for both small and large-scale environments. By following best practices and using the relevant commands, you can ensure optimal performance and reliability of your distributed storage system.
