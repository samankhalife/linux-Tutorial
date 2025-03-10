# corosync-cfgtool

`corosync-cfgtool` is a command-line utility provided with the Corosync cluster engine. It is used to inspect, diagnose, and display the runtime configuration and status of a Corosync cluster. This tool is invaluable for troubleshooting cluster communication issues, verifying node membership, and ensuring that the network interfaces and configuration settings are operating as expected.

## Purpose

- **Inspect Cluster Membership**:  
  Display the current view of cluster members and their statuses.

- **Troubleshooting**:  
  Diagnose issues related to cluster communication, node connectivity, and membership changes.

- **Configuration Verification**:  
  Confirm that the Corosync configuration is correctly applied and that the cluster interfaces are properly set up.

## Basic Syntax

```bash
corosync-cfgtool [options]
```

- **[options]**: Flags to display various aspects of the cluster status.

## Common Options and Their Usage

- **`-s`**:  
  **Display Membership Status**  
  Shows the current cluster membership, listing the node IDs and their states.

  ```bash
  corosync-cfgtool -s
  ```

- **`-S`**:  
  **Show Detailed Node Status**  
  Provides an extended view of the cluster nodes, including quorum information and additional status details.

  ```bash
  corosync-cfgtool -S
  ```

- **`-i`**:  
  **Display Interface Information**  
  Lists the network interfaces used by Corosync, along with their addresses and ports. This is useful for verifying that the correct communication channels are active.

  ```bash
  corosync-cfgtool -i
  ```

- **`-n`**:  
  **Display Local Node Information**  
  Shows the node ID and name of the local system, helping to quickly identify the current node in the cluster.

  ```bash
  corosync-cfgtool -n
  ```

## Example Usage

1. **Viewing Cluster Membership**

   ```bash
   corosync-cfgtool -s
   ```

   *Output*:  
   This command outputs a summary of the current cluster membership, listing each node by its ID and showing whether it is active in the current cluster view.

2. **Displaying Detailed Node Status**

   ```bash
   corosync-cfgtool -S
   ```

   *Output*:  
   This provides a detailed breakdown of node status, which can include quorum information and node health indicators.

3. **Inspecting Network Interfaces**

   ```bash
   corosync-cfgtool -i
   ```

   *Output*:  
   This command lists the network interfaces that Corosync uses, displaying relevant information such as IP addresses and port numbers. It’s helpful for verifying that the cluster’s communication channels are correctly configured.

## Best Practices

- **Regular Monitoring**:  
  Use `corosync-cfgtool` as part of routine cluster monitoring to ensure that all nodes remain properly connected and that the cluster membership is as expected.

- **Troubleshooting Integration**:  
  When issues arise (e.g., unexpected node dropouts or communication delays), incorporate `corosync-cfgtool` into your diagnostic process to quickly pinpoint problems.

- **Cross-Reference Logs**:  
  Compare the tool’s output with system logs and other diagnostic utilities (such as `corosync.log`) to get a comprehensive view of cluster health and communication.

## Conclusion

`corosync-cfgtool` is an essential utility for administrators managing Corosync clusters. It offers a straightforward way to view real-time cluster membership, network interface configurations, and detailed node statuses. Leveraging this tool helps ensure that the cluster is correctly configured and operating smoothly, ultimately contributing to a stable and highly available cluster environment.
