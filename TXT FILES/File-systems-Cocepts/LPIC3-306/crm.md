# crm
**crm** is a command-line interface traditionally used to manage and monitor Pacemaker clusters. It is part of the CRM Shell (crmsh) toolkit, which provides administrators with an interactive environment for configuring, controlling, and viewing the status of high-availability cluster resources.



## Overview

- **Legacy and Interactive Interface:**  
  `crm` offers an interactive shell where administrators can enter commands to configure the cluster, modify resource definitions, and query the cluster’s status.
  
- **Complementary Tools:**  
  While tools like `pcs` have become popular for cluster management, `crm` (and related commands such as `crm_mon` and `crm_resource`) are still used in many environments, especially those with legacy setups or where the CRM Shell is preferred.



## Purpose

- **Configuration Management:**  
  Use `crm` to create, modify, and delete cluster resources and constraints. This includes setting resource parameters, defining ordering and colocation constraints, and configuring fencing devices.
  
- **Monitoring:**  
  The interactive shell can be used to display real-time cluster status, including node states, resource statuses, and recent cluster events.
  
- **Troubleshooting:**  
  It provides commands for diagnosing cluster issues, reviewing logs, and verifying that the cluster configuration matches the desired state.



## Basic Syntax

In interactive mode, you launch the shell simply by typing:

```bash
crm
```

Once inside the shell, you can execute various commands, for example:

- **Configure the Cluster:**
  ```crm
  configure edit
  ```
  This command opens the current cluster configuration in an editor.

- **Show Cluster Status:**
  ```crm
  status
  ```
  Displays a summary of the current cluster status, including nodes, resources, and any issues.

- **Manage Resources:**
  ```crm
  resource status <resource_name>
  ```
  Queries the status of a specific cluster resource.

- **Exit the Shell:**
  ```crm
  exit
  ```



## Common Commands and Subcommands

- **crm configure:**  
  Manage the cluster configuration. You can use commands like `crm configure show` to display the configuration, or `crm configure edit` to modify it interactively.

- **crm_mon:**  
  Though available as a separate command, `crm_mon` is often invoked within the CRM Shell to monitor cluster status in real time.

- **crm_resource:**  
  Query and manage individual cluster resources, for example, starting, stopping, or restarting a resource.

- **crm_status:**  
  Provides a high-level view of the cluster, showing resource and node status along with any constraint violations or fencing events.



## Example Usage

1. **Launch the CRM Shell:**
   ```bash
   crm
   ```
   You’ll see a prompt where you can enter commands.

2. **Display Current Cluster Configuration:**
   ```crm
   configure show
   ```

3. **Edit Cluster Configuration:**
   ```crm
   configure edit
   ```
   This opens an editor where you can make configuration changes.

4. **Check Cluster Status:**
   ```crm
   status
   ```
   This displays a summary of nodes, resources, and recent events.

5. **Manage a Specific Resource:**
   ```crm
   resource status my-resource
   ```
   This queries the status of a resource named "my-resource".



## Conclusion

The **crm** command provides a flexible, interactive interface for managing Pacemaker clusters. While newer tools like `pcs` have gained popularity, `crm` remains a powerful option—especially in legacy environments or for administrators who prefer an interactive shell for cluster configuration and troubleshooting. It covers tasks from configuration management to real-time monitoring and resource control, making it a valuable tool in high-availability cluster administration.
