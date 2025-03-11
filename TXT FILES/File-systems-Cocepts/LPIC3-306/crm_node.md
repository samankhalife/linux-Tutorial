# crm_node

`crm_node` is a command-line tool from the crmsh suite used to query and manage node information in Pacemaker-based clusters. It focuses on listing cluster nodes, displaying their status, and sometimes allowing for basic node-level operations or attribute adjustments. This tool helps administrators verify the cluster membership and diagnose node-related issues.



## Purpose

- **Node Querying:**  
  Retrieve and display a list of nodes that are part of the cluster, along with their status (e.g., online, standby, offline).

- **Cluster Health Monitoring:**  
  Quickly assess the overall health of cluster nodes, which is essential for troubleshooting and ensuring that the cluster maintains quorum.

- **Node Management:**  
  In some cases, it may allow for basic management operations such as setting a node into standby mode or querying node attributes.



## Basic Syntax

```bash
crm_node [options] [command] [arguments]
```

### Common Operations

- **Listing Nodes:**
  ```bash
  crm_node --list
  ```
  This command outputs a list of all nodes currently recognized in the cluster.

- **Querying Node Status:**
  ```bash
  crm_node --status <node_name>
  ```
  Replace `<node_name>` with the name or identifier of the node to display detailed status information, such as whether the node is online, its current role, and any relevant attributes.

- **Help and Documentation:**
  ```bash
  crm_node --help
  ```
  Displays available commands, options, and usage details for the tool.



## Example Usage

1. **List All Nodes in the Cluster:**
   ```bash
   crm_node --list
   ```
   This command shows a summary of each node's presence in the cluster, making it easier to identify nodes that may be offline or not responding.

2. **Display Detailed Status for a Specific Node:**
   ```bash
   crm_node --status node1
   ```
   Replace `node1` with the actual node name to see more detailed information such as the node's connectivity, roles, and any attributes set for that node.



## Conclusion

`crm_node` is an essential tool for cluster administrators working with Pacemaker-managed environments. It provides a straightforward way to monitor and verify the nodes within a cluster, ensuring that all members are operating correctly and contributing to cluster quorum. For further details or advanced usage, you can refer to the built-in help documentation by running:
```bash
crm_node --help
```

This tool, alongside other crmsh utilities, helps maintain the overall health and stability of high-availability clusters by giving administrators direct insight into node status and configuration.
