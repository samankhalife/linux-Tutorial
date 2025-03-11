# ocf:pacemaker:ocfSysInfo

**ocf:pacemaker:ocfSysInfo** appears to be an OCF-compliant resource agent designed for use in Pacemaker-managed clusters to collect and report system information from a node. In many high-availability environments, such an agent would be used to monitor key system metrics (like CPU load, memory usage, disk space, uptime, etc.) and make that data available to the cluster manager.



## Purpose

- **System Monitoring:**  
  Collects real-time data about a node’s resource usage and operational state. This can include metrics such as CPU utilization, memory consumption, disk usage, and load averages.

- **Decision Support:**  
  Provides critical system information that the cluster management system (Pacemaker) can use to decide on resource allocation, failover actions, or load-balancing measures.

- **Health Checks:**  
  By monitoring system metrics, the agent can help detect abnormal conditions (e.g., excessive load or low available memory) that might indicate a node is becoming unstable.



## Expected Operations

Like most OCF resource agents, **ocf:pacemaker:ocfSysInfo** likely supports the standard set of operations:

- **start:**  
  Initializes the system information collection on the node.

- **stop:**  
  Stops any monitoring or data collection processes.

- **monitor:**  
  Periodically checks and reports the node’s system metrics. If the metrics fall outside of predefined thresholds, the monitor operation may return an error status to inform Pacemaker of potential issues.

- **meta-data:**  
  Provides an XML description of the resource agent’s supported parameters, operations, and default values. This metadata is useful for administrators to understand what can be configured (for example, which metrics to collect or threshold values).



## Example (Hypothetical)

A cluster administrator might configure the resource agent in a Pacemaker cluster using a command-line tool such as `pcs` like this:

```bash
pcs resource create SysInfo ocf:pacemaker:ocfSysInfo \
    cpu_threshold=80 memory_threshold=90 poll_interval=30 \
    op monitor interval=30s
```

In this hypothetical example:

- **cpu_threshold** and **memory_threshold** could be parameters defining what is considered a critical load.
- **poll_interval** sets how frequently the agent checks the system metrics.
- The `monitor` operation runs every 30 seconds to ensure the node’s health.



## Best Practices

- **Test in a Non-Production Environment:**  
  Because official details are sparse, test the agent’s behavior in a controlled environment to understand exactly which metrics are collected and how it signals failures.

- **Review Meta-Data:**  
  Use the meta-data operation (if available) to see all supported parameters. For example:
  ```bash
  crm ra metadata ocf:pacemaker:ocfSysInfo
  ```
  This can provide clues to the available settings and expected behaviors.

- **Integration with Other Monitoring:**  
  Consider using this agent alongside other monitoring tools to get a comprehensive view of system health.



## Conclusion

While specific official documentation for **ocf:pacemaker:ocfSysInfo** is not readily available, its name suggests it is intended to provide system utilization and health information in a Pacemaker cluster. It would follow the typical OCF resource agent model, supporting operations like start, stop, monitor, and meta-data, and allowing administrators to define thresholds and polling intervals for system metrics.

If you’re planning to use this agent, I recommend examining its metadata output and testing it in your environment to confirm its capabilities and ensure it meets your monitoring needs.
