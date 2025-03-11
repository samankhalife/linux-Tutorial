# corosync-quorumtool

`corosync-quorumtool` is a command-line utility used to query and manage the quorum state in a Corosync-based cluster. It allows you to check the quorum status, identify the cluster's quorum members, and display the current voting status. This tool is especially useful for diagnosing quorum-related issues and ensuring that your cluster has an active majority of nodes required for proper operation.

## Purpose

- **Monitor Quorum Status:**  
  Provides real-time information about the quorum status in a Corosync cluster, including the number of nodes in the quorum and the current leader.

- **Diagnose Quorum Failures:**  
  Helps identify quorum issues by displaying which nodes are currently in or out of quorum, making it easier to troubleshoot cluster communication problems.

- **Display Cluster Members:**  
  Lists the nodes participating in the cluster and their status with respect to quorum.

## Basic Syntax

```bash
corosync-quorumtool [OPTIONS]
```

- **No Arguments:**  
  Running the tool without any options shows the current quorum status.

  Example:
  ```bash
  corosync-quorumtool
  ```

- **Display Quorum Information:**  
  To get the quorum information, including the number of nodes in quorum, the tool outputs a status message.

  Example output:
  ```bash
  Quorum information:
  -------------------
  Last updated:     Thu Mar 10 13:17:31 2025
  Last change:      Thu Mar 10 13:17:30 2025
  Cluster name:     corosync
  Membership information:
   Member ID: 0 (node1)
     Status: in quorum
   Member ID: 1 (node2)
     Status: in quorum
   Member ID: 2 (node3)
     Status: in quorum
  ```

## Common Options

- **-v, --verbose**  
  Display detailed quorum information, including the status of all nodes.

  Example:
  ```bash
  corosync-quorumtool -v
  ```

- **-h, --help**  
  Show help information about the command.

  Example:
  ```bash
  corosync-quorumtool --help
  ```

## Example Usage

1. **Check Quorum Status**

   ```bash
   corosync-quorumtool
   ```
   This command provides the current quorum status of the cluster, listing all nodes and whether they are in quorum or not.

2. **Verbose Quorum Information**

   ```bash
   corosync-quorumtool -v
   ```
   This command provides a more detailed view, including the cluster's voting members and their states.

3. **Check Quorum after a Node Failure**

   If a node fails and the cluster may have lost quorum, running this command helps identify which nodes are still part of the quorum and which are out of it.

## Best Practices

- **Monitor Quorum Regularly:**  
  Regularly check the quorum status to ensure your cluster remains healthy, especially in larger clusters or in environments with frequent node additions or failures.

- **Use During Troubleshooting:**  
  In case of a failure or issues with cluster communication, `corosync-quorumtool` can be used to quickly determine whether quorum has been lost and which nodes are still part of the quorum.

- **Ensure Proper Node Configuration:**  
  Properly configure your nodes to avoid split-brain scenarios and ensure that a majority of nodes are always in quorum.

## Conclusion

`corosync-quorumtool` is an essential tool for maintaining the health and stability of a Corosync-based cluster. It enables administrators to check quorum status, view membership details, and diagnose quorum-related issues, ensuring that the cluster remains in a consistent and highly available state.
