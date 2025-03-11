# crm_attribute

`crm_attribute` is a command-line tool from the crmsh (Cluster Resource Manager Shell) suite used in Pacemaker clusters. It allows administrators to query, set, and remove dynamic attributes stored in the Cluster Information Base (CIB). These attributes can be used to influence cluster behavior, store configuration flags, or serve as markers for custom policies.



## Purpose

- **Dynamic Configuration:**  
  Modify and update cluster-wide or node-specific attributes on the fly, which can affect resource allocation, priority, or other policy decisions.

- **Monitoring and Troubleshooting:**  
  Query existing attributes to help diagnose cluster issues or verify that configuration changes have taken effect.

- **Automation and Scripting:**  
  Integrate attribute management into scripts for automated cluster management and operational tasks.



## Basic Syntax

```bash
crm_attribute [options]
```

Without any options, it may list current attributes. Common operations include listing, setting, and unsetting attributes.



## Common Options

- **`-l, --list`**  
  List all the currently defined attributes in the cluster.
  ```bash
  crm_attribute -l
  ```

- **`-S, --set`**  
  Set or update an attribute by specifying a key-value pair.
  ```bash
  crm_attribute -S attribute_name=attribute_value
  ```
  *Example:*
  ```bash
  crm_attribute -S maintenance=true
  ```
  This command sets the attribute `maintenance` to `true` across the cluster.

- **`-U, --unset`**  
  Remove a specific attribute.
  ```bash
  crm_attribute -U attribute_name
  ```
  *Example:*
  ```bash
  crm_attribute -U maintenance
  ```
  This command removes the `maintenance` attribute.

- **`-h, --help`**  
  Display help and usage information.
  ```bash
  crm_attribute --help
  ```



## Example Usage

1. **Listing Attributes:**  
   To view all current attributes in the cluster:
   ```bash
   crm_attribute -l
   ```

2. **Setting an Attribute:**  
   To mark the cluster as in maintenance mode:
   ```bash
   crm_attribute -S maintenance=true
   ```
   This attribute might be used by other policies or scripts to modify resource behavior during maintenance windows.

3. **Unsetting an Attribute:**  
   When maintenance is complete, remove the attribute:
   ```bash
   crm_attribute -U maintenance
   ```



## Conclusion

`crm_attribute` provides a flexible and dynamic way to manage custom attributes within a Pacemaker cluster. By allowing administrators to list, set, and remove attributes directly from the command line, it supports both manual configuration and automated scripts—helping to tailor cluster behavior and assist in monitoring and troubleshooting.
