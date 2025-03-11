# stonith_admin
`stonith_admin` is a command-line tool used for managing STONITH (Shoot The Other Node In The Head) devices and operations in **Pacemaker**-based high-availability clusters. It is used for querying, configuring, and triggering STONITH devices, which are responsible for fencing failed nodes to ensure cluster integrity.

### Syntax

```bash
stonith_admin [options] [commands]
```

### Common Options and Commands

- **-L, --list-all**  
  List all STONITH devices configured in the cluster.
  ```bash
  stonith_admin -L
  ```

- **-Q, --query**  
  Query the status of a specific STONITH device.
  ```bash
  stonith_admin -Q <device_name>
  ```

- **-H, --history**  
  Display the history of STONITH operations, showing which nodes were fenced and when.
  ```bash
  stonith_admin -H
  ```

- **-F, --fence**  
  Fence (power off or reboot) a specific node in the cluster manually.
  ```bash
  stonith_admin -F <node_name>
  ```

- **-U, --unfence**  
  Unfence (re-enable) a specific node in the cluster.
  ```bash
  stonith_admin -U <node_name>
  ```

- **-R, --register**  
  Register a new STONITH device in the cluster. You can specify the STONITH agent (e.g., `external/ipmi`) and options for the agent.
  ```bash
  stonith_admin -R <device_name> --stonith-type=<agent> <options>
  ```

- **-D, --deregister**  
  Deregister (remove) a STONITH device from the cluster.
  ```bash
  stonith_admin -D <device_name>
  ```

- **-S, --status**  
  Display the status of all STONITH devices.
  ```bash
  stonith_admin -S
  ```

- **-t, --test**  
  Simulate a STONITH action without actually fencing a node.
  ```bash
  stonith_admin -t <node_name>
  ```

- **-v, --verbose**  
  Run the command with more detailed output.

### Example Usage

- List all STONITH devices in the cluster:
  ```bash
  stonith_admin -L
  ```

- Query a specific STONITH device (e.g., `my_stonith_device`):
  ```bash
  stonith_admin -Q my_stonith_device
  ```

- Fence (power off) a node named `node1`:
  ```bash
  stonith_admin -F node1
  ```

- Register a new STONITH device for IPMI-based fencing:
  ```bash
  stonith_admin -R my_ipmi_device --stonith-type=external/ipmi ipaddr=192.168.1.100 login=admin passwd=secret lanplus=1
  ```

- Display STONITH operation history:
  ```bash
  stonith_admin -H
  ```

### STONITH Agents

There are various STONITH agents available depending on the type of fencing hardware or software being used. Examples include:

- **external/ipmi**: For fencing via IPMI-based power management.
- **fence_vmware**: For fencing virtual machines using VMware tools.
- **fence_xvm**: For Xen-based virtualization environments.

Each agent requires specific parameters (e.g., IP address, login credentials, etc.) to interact with the fencing device.

### Conclusion

`stonith_admin` is an essential tool for managing fencing operations in a Pacemaker-based cluster. It provides mechanisms to manually fence nodes, query fencing devices, and maintain high availability by ensuring nodes that are misbehaving or failing are removed from the cluster to prevent data corruption or other issues.
