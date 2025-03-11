# crm_mon
`crm_mon` is a command-line monitoring tool that provides a real-time view of the status of a Pacemaker-based high-availability cluster. It is part of the crmsh (Cluster Resource Manager Shell) suite and is widely used to quickly assess cluster health, view resource statuses, and monitor node activity.



## Purpose

- **Real-Time Monitoring:**  
  `crm_mon` displays the current state of the cluster, including information about nodes, resources, constraints, and fencing events. This helps administrators keep an eye on cluster health and detect issues promptly.

- **Cluster Overview:**  
  The tool presents an aggregated view of cluster components—such as which nodes are online or offline, the status of individual resources, and any constraint or configuration problems—making it easier to diagnose potential issues.

- **Troubleshooting:**  
  By providing a clear snapshot of the cluster state, `crm_mon` is invaluable for troubleshooting and verifying that changes to cluster configuration have been successfully applied.



## Basic Syntax

```bash
crm_mon [options]
```

Without any options, `crm_mon` outputs a continuous display of cluster status in the terminal, updating at regular intervals.



## Common Options

- **`-1`**  
  Exit after the first full status display.  
  ```bash
  crm_mon -1
  ```

- **`-n`**  
  Display node names rather than node IDs.  
  ```bash
  crm_mon -n
  ```

- **`-A`**  
  Show additional attribute information about nodes and resources.  
  ```bash
  crm_mon -A
  ```

- **`-r`**  
  Include resource history information in the output.  
  ```bash
  crm_mon -r
  ```

- **`-i`**  
  Include detailed information on resource failures and pending operations.  
  ```bash
  crm_mon -i
  ```

- **`-d`**  
  Set the display delay (in seconds) for each update (default is typically a few seconds).  
  ```bash
  crm_mon -d 5
  ```

- **`-2`**  
  Similar to `-1` but refreshes twice before exiting.  
  ```bash
  crm_mon -2
  ```

- **`-V`**  
  Display the version of crm_mon.  
  ```bash
  crm_mon -V
  ```



## Example Usage

1. **One-Time Status Snapshot:**
   To display the current cluster status once and then exit:
   ```bash
   crm_mon -1
   ```
   This command is useful for scripting or for quickly checking the state of the cluster.

2. **Continuous Monitoring:**
   Running `crm_mon` without any options will provide a continuously updated view:
   ```bash
   crm_mon
   ```
   This displays an ongoing status screen that refreshes periodically, allowing you to watch for changes over time.

3. **Detailed Output with Node Names and History:**
   To get a more detailed report that shows node names and historical events:
   ```bash
   crm_mon -n -r
   ```
   This is helpful for in-depth troubleshooting and for understanding resource transitions.

4. **Setting a Custom Refresh Interval:**
   To refresh the display every 5 seconds:
   ```bash
   crm_mon -d 5
   ```



## Output Overview

The typical output of `crm_mon` includes:

- **Cluster Summary:**  
  Overall status of the cluster including quorum status, any errors, or pending actions.

- **Node Information:**  
  A list of cluster nodes showing their status (online, standby, or offline), IP addresses, and other attributes.

- **Resource Status:**  
  Status of each configured resource, including whether it is running, stopped, or in a failed state, along with its current location and any constraints affecting it.

- **Fencing and Constraint Details:**  
  Information about recent fencing events or resource ordering/colocation constraints that may affect resource placement.



## Conclusion

`crm_mon` is an essential tool for administrators managing Pacemaker clusters. It offers a clear and concise real-time view of cluster status, making it easier to monitor health, diagnose issues, and verify the effects of configuration changes. Whether used in interactive mode or integrated into monitoring scripts, `crm_mon` provides vital insights into the operational state of high-availability clusters.
