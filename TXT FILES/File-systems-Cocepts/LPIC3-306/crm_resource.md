# crm_resource

`crm_resource` is a command-line utility that is part of the crmsh (Cluster Resource Manager Shell) toolkit used to manage and interact with resources in a Pacemaker-managed high-availability cluster. It provides administrators with the ability to query the status of resources, as well as perform operations like starting, stopping, or restarting resources directly from the command line.



## Purpose

- **Resource Querying:**  
  `crm_resource` allows you to obtain detailed status information for individual cluster resources, including their current state, location, and any pending operations or failures.

- **Resource Control:**  
  In addition to status checks, it can be used to control resources by initiating actions such as starting, stopping, or restarting a resource, which is useful for troubleshooting or performing manual failovers.

- **Scripting and Automation:**  
  The command's output can be used in scripts to monitor cluster health and to trigger automated responses if certain resources are found to be in an unexpected state.



## Basic Syntax

```bash
crm_resource [options] <command> <resource_name>
```

- **Options:** Various options to control verbosity or output formatting.
- **Command:** The action to be performed (e.g., `status`, `start`, `stop`, `restart`).
- **Resource Name:** The name of the resource as defined in the cluster configuration.



## Common Commands

- **Query Resource Status:**

  ```bash
  crm_resource --resource <resource_name> --query
  ```

  *Example:*
  ```bash
  crm_resource --resource my-web-server --query
  ```
  This command returns the current status of the resource `my-web-server`, such as whether it is running, stopped, or in a failed state.

- **Start a Resource:**

  ```bash
  crm_resource --resource <resource_name> --action start
  ```

  *Example:*
  ```bash
  crm_resource --resource my-database --action start
  ```
  This initiates the start operation for the resource `my-database`.

- **Stop a Resource:**

  ```bash
  crm_resource --resource <resource_name> --action stop
  ```

  *Example:*
  ```bash
  crm_resource --resource my-database --action stop
  ```
  This stops the resource `my-database`.

- **Restart a Resource:**

  ```bash
  crm_resource --resource <resource_name> --action restart
  ```

  *Example:*
  ```bash
  crm_resource --resource my-app --action restart
  ```
  This command restarts the resource `my-app`.

- **Get Resource Metadata:**

  ```bash
  crm_resource --resource <resource_name> --meta-data
  ```

  *Example:*
  ```bash
  crm_resource --resource my-web-server --meta-data
  ```
  This displays the metadata and configuration details for `my-web-server`, providing insights into its configuration parameters and constraints.



## Example Workflow

1. **Check the status of a resource:**
   ```bash
   crm_resource --resource my-ip --query
   ```
   This helps determine if the resource is active, stopped, or in an error state.

2. **Restart a resource that is not performing correctly:**
   ```bash
   crm_resource --resource my-ip --action restart
   ```
   Restarting can often resolve transient issues.

3. **Retrieve metadata for troubleshooting:**
   ```bash
   crm_resource --resource my-ip --meta-data
   ```
   This command helps administrators understand the configuration details, which can be compared against expected settings when diagnosing issues.



## Conclusion

`crm_resource` is a versatile and essential tool for administrators managing Pacemaker clusters. It provides direct control over individual cluster resources, enabling effective monitoring, troubleshooting, and management through a consistent command-line interface. Whether you need to query resource status, start or stop resources, or examine detailed metadata, `crm_resource` helps ensure that your high-availability cluster operates smoothly and reliably.
