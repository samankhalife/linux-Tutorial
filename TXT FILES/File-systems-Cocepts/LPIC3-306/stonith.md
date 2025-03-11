# stonith
`stonith` stands for **Shoot The Other Node In The Head** and is a fencing mechanism used in high-availability clusters, particularly in **Pacemaker** and **Corosync** environments. The goal of STONITH is to forcibly restart or shut down a node that is behaving erratically or is unresponsive, ensuring the integrity of shared resources like databases or file systems. This is essential in preventing split-brain scenarios where two nodes think they are both the master node.

STONITH ensures that only one node can control a resource by powering off other nodes that may cause conflicts or have become unreachable.

### Purpose

- **Fencing Mechanism**:  
  It is a way of isolating and recovering from node failures by powering off or rebooting the failed node to protect data integrity and ensure high availability.

- **Prevent Split-Brain**:  
  By forcibly removing a malfunctioning node from the cluster, `stonith` prevents multiple nodes from accessing the same resources, avoiding corruption or data loss.

## STONITH Agents

STONITH agents are scripts or programs that implement the fencing mechanisms for various devices, including IPMI, power distribution units (PDUs), virtual machine hypervisors, and others. Each agent supports different parameters to manage fencing operations.

## Common Commands

In **Pacemaker**-based high-availability clusters, STONITH is integrated with tools like `crm`, `stonith_admin`, and `pcs`. Here are the key commands related to STONITH:

### stonith_admin

`stonith_admin` is used to manage STONITH devices in a Pacemaker cluster.

```bash
stonith_admin [options] [commands]
```

#### Common Options and Commands:

- **-L**  
  List all STONITH devices configured in the cluster:
  ```bash
  stonith_admin -L
  ```

- **-Q --query**  
  Query the status of a specific STONITH device:
  ```bash
  stonith_admin -Q my_stonith_device
  ```

- **-H --history**  
  Display the history of STONITH operations:
  ```bash
  stonith_admin -H
  ```

- **-F --fence**  
  Fence (power off or reboot) a specific node in the cluster:
  ```bash
  stonith_admin -F <node_name>
  ```

- **-R --register**  
  Register a new STONITH device in the cluster:
  ```bash
  stonith_admin -R <device_name> --stonith-type=external/ipmi ...
  ```

- **-U --unfence**  
  Unfence (re-enable) a node in the cluster after a fence action:
  ```bash
  stonith_admin -U <node_name>
  ```

### pcs stonith

**pcs** is a command-line tool to configure and manage cluster resources in Pacemaker. The `pcs` tool has STONITH-specific subcommands.

- **Create a STONITH device**:
  ```bash
  pcs stonith create <name> <stonith-agent> [options]
  ```
  Example:
  ```bash
  pcs stonith create my-fence-device fence_ipmilan ipaddr=192.168.1.10 login=root passwd=secret lanplus=1
  ```

- **List STONITH devices**:
  ```bash
  pcs stonith
  ```

- **Fencing a node**:
  ```bash
  pcs stonith fence <node_name>
  ```

- **Check STONITH status**:
  ```bash
  pcs status
  ```

## STONITH Configuration in Cluster

STONITH is configured in high-availability clusters using tools like Pacemaker, which rely on the fencing mechanism. The key components include:

- **STONITH Device**: The hardware or software that is used to fence a node.
- **STONITH Resource**: The configuration for a fencing device, added as a resource to the cluster.

Example configuration in Pacemaker with `pcs`:

```bash
pcs stonith create my-fence fence_ipmilan ipaddr=192.168.1.100 login=admin passwd=admin123 lanplus=1
pcs property set stonith-enabled=true
```

This will create a STONITH resource using the `fence_ipmilan` agent to control the IPMI-based power management for the cluster nodes.

## Example Scenario

1. **Node Failure**: If a node in the cluster becomes unresponsive or its communication fails, Pacemaker triggers a fencing operation via STONITH.
2. **STONITH Action**: The STONITH device (e.g., an IPMI power controller) will reboot or power off the faulty node.
3. **Node Recovery**: Once the node is restarted, it can rejoin the cluster after passing health checks.

## Conclusion

STONITH is a crucial component for ensuring the reliability and integrity of high-availability clusters by forcibly removing problematic nodes to prevent data corruption and split-brain situations. It's integrated with cluster management tools such as Pacemaker and Corosync, offering automated recovery mechanisms to maintain service availability.
