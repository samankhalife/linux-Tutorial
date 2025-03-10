# ceph.conf
The `ceph.conf` file is the primary configuration file for a Ceph cluster. It contains settings that define the behavior of the Ceph monitors, OSDs, metadata servers (MDS), and other Ceph daemons. The configuration file is typically located in `/etc/ceph/ceph.conf` on Ceph nodes.

Each section in `ceph.conf` is specified for different components, such as global settings that apply to all Ceph daemons, or specific settings for monitors, OSDs, and clients.

Below is an overview of the common sections and key options found in the `ceph.conf` file:

## Example of a Basic `ceph.conf` File

```ini
[global]
fsid = e4a89f8c-4a64-4df5-bcdf-e246b6f8120e
mon_initial_members = mon1, mon2, mon3
mon_host = 192.168.1.1, 192.168.1.2, 192.168.1.3
auth_cluster_required = cephx
auth_service_required = cephx
auth_client_required = cephx
osd_pool_default_size = 3
osd_pool_default_min_size = 2
osd_crush_chooseleaf_type = 1

[mon]
mon_allow_pool_delete = true

[osd]
osd_journal_size = 1024
osd_max_object_name_len = 256
osd_max_object_namespace_len = 64

[client]
log_file = /var/log/ceph/ceph.log
```

## Sections of the `ceph.conf` File

### 1. **[global]**
The `[global]` section contains settings that apply to all Ceph components (monitors, OSDs, MDS, clients, etc.). This is the most commonly used section and is essential for setting up cluster-wide options.

- **`fsid`**: The unique identifier for the Ceph cluster (UUID). This is automatically generated during the creation of the cluster.
  
  Example:
  ```ini
  fsid = e4a89f8c-4a64-4df5-bcdf-e246b6f8120e
  ```

- **`mon_initial_members`**: List of monitor nodes in the cluster. This is a comma-separated list of monitor names.
  
  Example:
  ```ini
  mon_initial_members = mon1, mon2, mon3
  ```

- **`mon_host`**: List of IP addresses or hostnames of the monitor nodes. This is a comma-separated list of addresses.
  
  Example:
  ```ini
  mon_host = 192.168.1.1, 192.168.1.2, 192.168.1.3
  ```

- **`auth_cluster_required`**, **`auth_service_required`**, **`auth_client_required`**: These options configure authentication for Ceph using `cephx`. All of these should typically be set to `cephx` for secure authentication.
  
  Example:
  ```ini
  auth_cluster_required = cephx
  auth_service_required = cephx
  auth_client_required = cephx
  ```

- **`osd_pool_default_size`**: The default replication size of a pool (i.e., how many copies of an object to store across OSDs).
  
  Example:
  ```ini
  osd_pool_default_size = 3
  ```

- **`osd_pool_default_min_size`**: The minimum number of replicas that a pool can have while still allowing I/O operations.
  
  Example:
  ```ini
  osd_pool_default_min_size = 2
  ```

- **`osd_crush_chooseleaf_type`**: Defines how the CRUSH algorithm selects OSDs for redundancy. Typically, `1` refers to selecting based on host level.

  Example:
  ```ini
  osd_crush_chooseleaf_type = 1
  ```

### 2. **[mon]**
The `[mon]` section defines settings specific to monitor nodes.

- **`mon_allow_pool_delete`**: This option allows pools to be deleted. Setting this to `true` is often necessary for testing or when managing the cluster.

  Example:
  ```ini
  mon_allow_pool_delete = true
  ```

### 3. **[osd]**
The `[osd]` section defines settings that apply specifically to OSD daemons. OSDs store the actual data and handle replication, recovery, and rebalancing.

- **`osd_journal_size`**: Specifies the size of the OSD journal in megabytes. The OSD journal is used to track writes before they are committed to disk. A larger journal size improves write performance but consumes more disk space.

  Example:
  ```ini
  osd_journal_size = 1024
  ```

- **`osd_max_object_name_len`**: Sets the maximum length for an object name in the OSD.

  Example:
  ```ini
  osd_max_object_name_len = 256
  ```

- **`osd_max_object_namespace_len`**: Sets the maximum length for an object namespace.

  Example:
  ```ini
  osd_max_object_namespace_len = 64
  ```


### 4. **[client]**
The `[client]` section defines settings for Ceph clients, which can include applications, user interfaces, and commands interacting with the Ceph cluster.

- **`log_file`**: Defines where client logs are stored. Useful for debugging and tracking client activity.
  
  Example:
  ```ini
  log_file = /var/log/ceph/ceph.log
  ```

### Additional Useful Options

- **`public_network`**: Defines the network used by public-facing Ceph components, such as monitors and clients. This network handles client traffic.

  Example:
  ```ini
  public_network = 192.168.1.0/24
  ```

- **`cluster_network`**: Defines the network used by the OSDs for replication and recovery traffic. It's recommended to separate the public and cluster networks for performance and security.

  Example:
  ```ini
  cluster_network = 10.0.0.0/24
  ```

- **`osd_crush_update_on_start`**: If set to `true`, OSDs update the CRUSH map when they start, which can be useful during recovery.

  Example:
  ```ini
  osd_crush_update_on_start = true
  ```


## Best Practices for `ceph.conf`

1. **Minimal Configuration**: Keep your `ceph.conf` minimal. Ceph has sensible defaults for many settings, so you should only modify options that are necessary for your deployment.
  
2. **Separate Networks**: Use separate public and cluster networks to improve performance and security, especially in large-scale deployments.

3. **Secure Authentication**: Always use `cephx` for cluster, service, and client authentication unless you have a very specific reason not to. It adds an additional layer of security to your cluster.

4. **Backup `ceph.conf`**: Ensure that you maintain a backup of the `ceph.conf` file, especially after making changes, so that you can restore it if needed.

5. **Tune for Your Environment**: Adjust parameters like `osd_journal_size`, replication size, and CRUSH rules according to the specific needs of your environment and workload.

## Conclusion

The `ceph.conf` file is essential for configuring and managing a Ceph cluster. By understanding its key sections and options, you can fine-tune your Ceph environment to optimize performance, availability, and security. The structure is simple, yet it provides great flexibility, allowing you to manage the behavior of all Ceph components with just a few lines of configuration.
