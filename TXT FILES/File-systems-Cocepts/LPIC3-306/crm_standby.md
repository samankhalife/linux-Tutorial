# crm_standby

`crm_standby` is a command from the crmsh (Cluster Resource Manager Shell) suite used in Pacemaker clusters. It is specifically designed to place a node into standby mode, effectively removing it from active resource allocation while keeping it in the cluster membership. This is useful for maintenance, upgrades, or troubleshooting without triggering unintended failover or resource reallocation.



## Purpose

- **Maintenance Mode:**  
  Puts a node into a dormant state so that no new resources are started on it. This allows administrators to perform maintenance or upgrades safely without affecting running services.

- **Prevent Resource Allocation:**  
  While in standby, the node will not be assigned resources by the cluster manager, ensuring that all critical workloads remain on active nodes.

- **Cluster Stability:**  
  Helps prevent split-brain scenarios or resource conflicts when a node is temporarily unable to handle its workload due to maintenance.



## Basic Syntax

In the crmsh environment, you can issue the command as follows:

```bash
crm_standby [options] <node_name>
```

- **`<node_name>`**: The identifier of the node you wish to put into standby mode.



## Example Usage

1. **Place a Node in Standby Mode:**
   ```bash
   crm_standby node1
   ```
   This command places the node `node1` into standby mode, ensuring that it will not be allocated any cluster resources until it is brought back online.

2. **Bringing a Node Out of Standby:**
   Once maintenance or testing is complete, you can remove the node from standby mode by using the corresponding command:
   ```bash
   crm_standby -u node1
   ```
   Here, the `-u` (or `--unstandby`) option is used to bring the node `node1` back to active status, allowing the cluster manager to reassign resources to it.



## Considerations

- **Resource Relocation:**  
  When a node is placed into standby, its resources are typically relocated to other active nodes to maintain service availability. This process should be monitored to ensure that failover occurs smoothly.

- **Cluster Quorum:**  
  Ensure that placing a node in standby does not adversely affect cluster quorum, especially in smaller clusters where each node is critical.

- **Planned Maintenance:**  
  Always schedule and notify stakeholders before placing nodes in standby mode, as this might temporarily alter the resource distribution in your high-availability environment.



## Conclusion

`crm_standby` is an essential tool for managing maintenance and operational tasks in Pacemaker clusters. By allowing administrators to temporarily disable resource allocation on a node, it ensures that necessary maintenance can be performed without disrupting the overall cluster functionality. When used in conjunction with proper failover and recovery procedures, `crm_standby` helps maintain high availability and stability in critical environments.
