# ocf:pacemaker:HealthCPU
`ocf:pacemaker:HealthCPU` is an OCF-compliant resource agent designed for use within Pacemaker clusters to monitor the CPU health of a node. Its primary role is to continuously track CPU utilization and related metrics, enabling the cluster to detect when a node's CPU is under excessive load or otherwise unhealthy. This information can be used to trigger corrective actions, such as resource relocation, load balancing, or even node fencing if the situation deteriorates.



## Purpose

- **Monitor CPU Utilization:**  
  Regularly check the CPU load and performance on a node to ensure it remains within defined healthy thresholds.

- **Trigger Alerts:**  
  If the CPU usage exceeds a preconfigured threshold (for example, 80% or 90%), the agent can signal a fault condition, allowing the cluster manager to take appropriate actions.

- **Support Cluster Decisions:**  
  The CPU health data provided by this agent may be used in automated decision-making by Pacemaker, for instance, to decide if a node should be taken out of service or if workloads need to be rebalanced.



## Standard Operations

Like other OCF resource agents, `ocf:pacemaker:HealthCPU` supports the typical set of operations:

- **start:**  
  Initializes the CPU health monitoring on the node.

- **stop:**  
  Stops the monitoring process.

- **monitor:**  
  Periodically assesses CPU utilization. If the CPU usage is within acceptable limits, it returns a success status; if thresholds are exceeded, it returns a failure or warning status.

- **meta-data:**  
  Provides an XML description of the resource agent, including supported parameters, operations, and default values. This can be used by cluster management tools to help configure the resource.



## Key Parameters

While exact parameters may vary based on implementation, typical settings might include:

- **cpu_threshold:**  
  The maximum allowable CPU utilization percentage (e.g., `80` for 80%). Exceeding this threshold might indicate an overloaded node.

- **poll_interval:**  
  The frequency (in seconds) at which the agent polls the system to check CPU metrics.

- **sample_count:**  
  The number of samples to consider when averaging CPU load to avoid transient spikes from triggering false alarms.

Additional parameters may also be available depending on how the agent gathers CPU metrics (for example, via system load averages, utilization from `/proc/stat`, or other system monitoring interfaces).



## Example Usage

A typical configuration in a Pacemaker cluster using the `pcs` tool might look like this:

```bash
pcs resource create HealthCPU ocf:pacemaker:HealthCPU \
    cpu_threshold=80 poll_interval=30 op monitor interval=30s
```

This command creates a resource named `HealthCPU` that:
- Monitors CPU usage.
- Flags a condition if CPU utilization exceeds 80%.
- Polls the system every 30 seconds.



## Best Practices

- **Tune Thresholds:**  
  Adjust the `cpu_threshold` based on the expected workload of your node. For nodes under heavy load by design, a higher threshold may be more appropriate.

- **Combine with Other Metrics:**  
  Consider integrating CPU health monitoring with other resource metrics (e.g., memory or disk I/O) for a more comprehensive view of node health.

- **Review Metadata:**  
  Use the meta-data operation to confirm which parameters are supported and to understand default values. For example:
  ```bash
  crm ra metadata ocf:pacemaker:HealthCPU
  ```

- **Test in a Staging Environment:**  
  Before deploying in production, test the resource agent in a controlled environment to ensure that its monitoring and threshold logic align with your cluster’s operational requirements.



## Conclusion

`ocf:pacemaker:HealthCPU` is a specialized resource agent that plays an important role in maintaining the health and stability of a high-availability cluster by monitoring CPU utilization. By providing timely alerts when CPU usage exceeds predefined thresholds, it helps administrators proactively manage node performance and ensure that resources are balanced across the cluster. This agent follows the standard OCF resource agent model, making it compatible with Pacemaker's broader suite of cluster management tools and policies.
