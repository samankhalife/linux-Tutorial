# corosync.conf

**`corosync.conf`** is the main configuration file for the Corosync cluster engine. This file is used to define how nodes communicate, manage cluster membership, handle message timeouts, and log events. It is typically located in `/etc/corosync/corosync.conf` and plays a crucial role in establishing a reliable and high-availability cluster environment.

## Key Sections and Settings

### 1. **totem**

The `totem` section defines the core communication settings for the cluster. Key parameters include:
- **version:**  
  The version of the Totem protocol.  
  Example: `version: 2`
- **cluster_name:**  
  A unique identifier for the cluster.
- **transport:**  
  The network transport mechanism (usually `udpu` for UDP unicast or `udpu` for UDP multicast).
- **interface:**  
  Specifies the network interface to be used (including bind address and port).  
  Example:
  ```ini
  interface {
      ringnumber: 0
      bindnetaddr: 192.168.1.0
      mcastaddr: 226.94.1.1
      mcastport: 5405
  }
  ```
- **token:**  
  Defines timeout and retransmission settings, like `token: 5000` (milliseconds).
- **token_retransmits_before_loss_const:**  
  Specifies how many token retransmissions are allowed before considering a message lost.

### 2. **nodelist**

The `nodelist` section enumerates all the nodes in the cluster. Each node is specified with:
- **nodeid:**  
  A unique identifier for the node.
- **name:**  
  A human-readable name for the node.
- **ring0_addr:**  
  The IP address used for inter-node communication.
  
Example:
```ini
nodelist {
    node {
        nodeid: 1
        name: node1
        ring0_addr: 192.168.1.101
    }
    node {
        nodeid: 2
        name: node2
        ring0_addr: 192.168.1.102
    }
}
```

### 3. **quorum**

The `quorum` section defines settings related to cluster quorum:
- **provider:**  
  Determines how quorum is calculated.
- **two_node:**  
  Special settings for two-node clusters (if applicable).
  
Example:
```ini
quorum {
    provider: corosync_votequorum
    two_node: 1
}
```

### 4. **logging**

The `logging` section configures how Corosync logs events:
- **to_syslog:**  
  Specifies whether logs should be sent to syslog.
- **timestamp:**  
  Option to include timestamps in logs.
- **debug:**  
  Enables or disables debug logging.
  
Example:
```ini
logging {
    to_syslog: yes
    timestamp: on
    debug: off
}
```



## Best Practices

- **Consistency:**  
  Ensure that all nodes in the cluster have an identical `corosync.conf` to avoid communication problems.
- **Network Configuration:**  
  Set the `bindnetaddr` correctly to match your network topology.
- **Timeout Tuning:**  
  Adjust token and retransmission settings based on your network's latency to optimize performance.
- **Backup:**  
  Always back up the `corosync.conf` file before making changes.



## Conclusion

The **`corosync.conf`** file is vital for configuring the Corosync cluster engine, dictating how nodes communicate and maintain cluster membership. Its sections—such as `totem`, `nodelist`, `quorum`, and `logging`—provide comprehensive control over the behavior of the cluster, enabling high availability and reliable performance in distributed systems.

For further details, you might refer to official Corosync documentation or community resources that provide in-depth guides on configuring each section.

citedrbdwiki-corosyncconf
