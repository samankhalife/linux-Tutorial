# pcs
**`pcs`** is a command-line tool used to manage and configure high-availability clusters based on **Pacemaker** and **Corosync**. It allows administrators to manage cluster nodes, configure resources, control failover and fencing, and more. Below are some common **`pcs`** commands and their subcommands:

### Cluster Management
- **`pcs cluster start [nodes]`**  
  Starts the Pacemaker cluster on specified nodes.
  ```bash
  pcs cluster start node1 node2
  ```

- **`pcs cluster stop [nodes]`**  
  Stops the cluster on the specified nodes.
  ```bash
  pcs cluster stop node1 node2
  ```

- **`pcs cluster status`**  
  Displays the status of the entire cluster.
  ```bash
  pcs cluster status
  ```

- **`pcs cluster enable --all`**  
  Enables the cluster to automatically start on boot for all nodes.
  ```bash
  pcs cluster enable --all
  ```

- **`pcs cluster disable --all`**  
  Disables the cluster from starting automatically on boot.
  ```bash
  pcs cluster disable --all
  ```

- **`pcs cluster destroy`**  
  Removes the cluster configuration, essentially destroying the cluster setup.
  ```bash
  pcs cluster destroy
  ```

### Resource Management
- **`pcs resource create [resource-name] [type] [options]`**  
  Creates a resource in the cluster. Resources can be services, IP addresses, filesystems, or other cluster-managed entities.
  ```bash
  pcs resource create my-ip ocf:heartbeat:IPaddr2 ip=192.168.1.100 cidr_netmask=24
  ```

- **`pcs resource delete [resource-name]`**  
  Deletes a resource from the cluster.
  ```bash
  pcs resource delete my-ip
  ```

- **`pcs resource restart [resource-name]`**  
  Restarts a specific resource.
  ```bash
  pcs resource restart my-ip
  ```

- **`pcs resource status`**  
  Displays the status of all resources.
  ```bash
  pcs resource status
  ```

- **`pcs resource manage [resource-name]`**  
  Enables manual management of the resource, preventing Pacemaker from managing it automatically.
  ```bash
  pcs resource manage my-ip
  ```

- **`pcs resource unmanage [resource-name]`**  
  Reverts a manually managed resource back to automatic management by Pacemaker.
  ```bash
  pcs resource unmanage my-ip
  ```

### Node Management
- **`pcs node standby [node-name]`**  
  Places the specified node into standby mode, preventing it from hosting resources.
  ```bash
  pcs node standby node1
  ```

- **`pcs node unstandby [node-name]`**  
  Removes the node from standby mode, allowing it to host resources again.
  ```bash
  pcs node unstandby node1
  ```

- **`pcs node remove [node-name]`**  
  Removes a node from the cluster.
  ```bash
  pcs node remove node2
  ```

### Fencing and STONITH
- **`pcs stonith create [name] [type] [options]`**  
  Creates a STONITH (Shoot The Other Node In The Head) fencing device to reboot or power off a node in case of failure.
  ```bash
  pcs stonith create fence-device fence_ipmilan ipaddr=192.168.1.10 login=root passwd=password pcmk_host_list=node1
  ```

- **`pcs stonith delete [stonith-device-name]`**  
  Deletes a STONITH device.
  ```bash
  pcs stonith delete fence-device
  ```

- **`pcs stonith status`**  
  Displays the status of all STONITH devices.
  ```bash
  pcs stonith status
  ```

### Constraint Management
- **`pcs constraint location [resource-name] prefers [node-name]`**  
  Sets a location preference for a resource to run on a particular node.
  ```bash
  pcs constraint location my-ip prefers node1=100
  ```

- **`pcs constraint colocation add [resource1] with [resource2]`**  
  Ensures that two resources run on the same node (or different nodes using a negative score).
  ```bash
  pcs constraint colocation add app with my-ip
  ```

- **`pcs constraint order start [resource1] then [resource2]`**  
  Sets the order in which resources are started or stopped.
  ```bash
  pcs constraint order start my-ip then app
  ```

### Quorum and Status
- **`pcs quorum status`**  
  Shows quorum status for the cluster.
  ```bash
  pcs quorum status
  ```

- **`pcs status`**  
  Displays a high-level overview of the cluster, including nodes, resources, and fencing devices.
  ```bash
  pcs status
  ```

- **`pcs config`**  
  Shows the current cluster configuration.
  ```bash
  pcs config
  ```

### Property and Options Management
- **`pcs property set [property-name]=[value]`**  
  Sets cluster-wide properties, such as enabling or disabling STONITH.
  ```bash
  pcs property set stonith-enabled=false
  ```

- **`pcs resource defaults`**  
  Displays or sets default values for resource options such as timeouts or monitoring intervals.
  ```bash
  pcs resource defaults resource-stickiness=100
  ```



**`pcs`** is a comprehensive tool for managing Pacemaker/Corosync-based high-availability clusters. It provides rich functionality to configure, monitor, and troubleshoot clusters effectively, ensuring uptime and reliability in critical systems.
