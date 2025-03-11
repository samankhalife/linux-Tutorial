# ocf:pacemaker:ping

The **ocf:pacemaker:ping** resource agent is an OCF-compliant (Open Cluster Framework) agent designed to monitor network connectivity by using the standard ping utility. It is typically deployed in Pacemaker-managed clusters to verify that a target host (often another cluster node or a critical network endpoint) is reachable. If the ping check fails, the resource agent signals a failure, which can then trigger recovery or fencing operations.


## Purpose

- **Connectivity Monitoring:**  
  Periodically sends ICMP echo requests (ping) to a specified host to ensure that the network connection is active.

- **Cluster Health:**  
  Helps in determining if a remote host or critical network path is available. In a cluster, this can be used to monitor node availability or to trigger automated responses if connectivity is lost.

- **Failure Detection:**  
  Supports cluster failover by detecting when a host becomes unreachable, allowing the cluster to take corrective actions (such as resource relocation or node fencing).



## Key Parameters

- **host (required):**  
  The IP address or hostname of the target to be pinged.
  
- **count (optional):**  
  The number of ping packets to send per check (default is typically 1 or 3, depending on the implementation).

- **timeout (optional):**  
  The maximum time (in seconds) to wait for a ping response before declaring a failure.

- **ping_options (optional):**  
  Additional options to be passed to the underlying ping command for fine-tuning its behavior.



## Standard Operations

Like other OCF resource agents, **ocf:pacemaker:ping** supports a standard set of operations:

- **start/stop:**  
  Although ping is primarily used for monitoring, the start and stop operations can be used to initialize or disable the monitoring process if required.

- **monitor:**  
  The monitor operation periodically executes the ping command to verify connectivity. A successful ping returns an OCF_SUCCESS status, while a failure returns an error status.

- **meta-data:**  
  Provides an XML description of the resource agent, including supported parameters and default values. You can view this metadata with a command such as:
  
  ```bash
  crm ra metadata ocf:pacemaker:ping
  ```



## Example Usage in a Cluster

In a Pacemaker-managed cluster, you might create a ping resource with the following command:

```bash
pcs resource create ping_resource ocf:pacemaker:ping host=192.168.1.100 count=3 timeout=5 op monitor interval=30s
```

This command does the following:

- Creates a resource named `ping_resource` using the **ocf:pacemaker:ping** agent.
- Configures it to ping the host at `192.168.1.100` using 3 packets with a 5-second timeout.
- Sets up a monitoring operation that checks connectivity every 30 seconds.



## Best Practices

- **Parameter Tuning:**  
  Adjust the `count` and `timeout` parameters to suit your network conditions. A higher count can reduce false positives in unstable networks, but may also delay failure detection.

- **Integration with Cluster Policies:**  
  Use the ping resource as part of a broader strategy to monitor node connectivity or critical network paths. Combine it with constraints and recovery policies in Pacemaker to automate failover.

- **Resource Agent Metadata:**  
  Always review the metadata provided by the resource agent (via the meta-data operation) to understand the available parameters and defaults before deploying in production.



## Conclusion

The **ocf:pacemaker:ping** resource agent is a lightweight and effective tool for monitoring network connectivity within a high-availability cluster. By leveraging standard ICMP ping operations, it provides real-time insights into the reachability of critical hosts, thereby helping to maintain overall cluster health and triggering automated recovery actions when connectivity issues are detected.
