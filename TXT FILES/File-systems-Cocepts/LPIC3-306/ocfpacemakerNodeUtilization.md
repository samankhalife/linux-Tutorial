# ocf:pacemaker:NodeUtilization
`ocf:pacemaker:NodeUtilization` is an OCF-compliant resource agent intended for use in Pacemaker clusters to monitor a node’s resource utilization. Although detailed official documentation is scarce, this agent is generally designed to track key metrics—such as CPU usage, memory consumption, and possibly disk I/O or network load—to help determine if a node is overutilized. This information can be used to trigger automated actions (like load redistribution or even initiating failover procedures) when resource usage exceeds defined thresholds.



## Purpose

- **Resource Monitoring:**  
  Continuously measure utilization metrics (e.g., CPU and memory) on a cluster node.
  
- **Threshold-Based Alerts:**  
  Enable configuration of thresholds (for example, 80% CPU or 90% memory usage) that, when exceeded, can trigger alerts or resource management actions.
  
- **Cluster Decision Making:**  
  Provide data that may be used by cluster management tools (like Pacemaker) to make decisions about rebalancing workloads or relocating resources.



## Key Features and Operations

### Standard Operations

Like most OCF resource agents, `ocf:pacemaker:NodeUtilization` supports the following operations:

- **start:**  
  Initializes the monitoring process on the node.

- **stop:**  
  Terminates the monitoring process.

- **monitor:**  
  Periodically checks the node’s utilization metrics against the configured thresholds and returns a status:
  - **OCF_SUCCESS** if metrics are within acceptable limits.
  - An error status (e.g., OCF_NOT_RUNNING or a custom failure code) if thresholds are exceeded.

- **meta-data:**  
  Outputs an XML description of the resource agent, including supported parameters and default values.

### Common Parameters (Illustrative)

*Note: The exact parameters may vary based on implementation or custom versions of this agent.*

- **cpu_threshold:**  
  A percentage (e.g., `80`) indicating the maximum acceptable CPU utilization.

- **memory_threshold:**  
  A percentage (e.g., `90`) for memory usage beyond which the agent may signal a warning or failure.

- **poll_interval:**  
  The interval (in seconds) at which the agent polls resource utilization metrics.

- **disk_threshold:**  
  (If supported) The disk utilization percentage threshold.



## Example Usage

A typical configuration in a Pacemaker cluster using the `pcs` tool might look like this:

```bash
pcs resource create NodeUtilization ocf:pacemaker:NodeUtilization \
  cpu_threshold=80 memory_threshold=90 poll_interval=30 \
  op monitor interval=30s
```

This command creates a resource named `NodeUtilization` that:
- Monitors CPU and memory usage.
- Flags a condition if CPU usage exceeds 80% or memory usage exceeds 90%.
- Polls every 30 seconds.



## Conclusion

While the official documentation for `ocf:pacemaker:NodeUtilization` is limited, its role in a Pacemaker-managed cluster is to provide real-time insights into a node's resource consumption. By setting utilization thresholds, cluster administrators can proactively manage load and maintain high availability. This resource agent fits into the standard OCF framework, supporting common operations like start, stop, monitor, and meta-data, which makes it compatible with cluster management tools and policies.

If you are planning to deploy or troubleshoot this resource agent, reviewing the agent’s meta-data (using the `meta-data` operation) and testing its behavior in a controlled environment is recommended to ensure it meets your cluster’s requirements.
