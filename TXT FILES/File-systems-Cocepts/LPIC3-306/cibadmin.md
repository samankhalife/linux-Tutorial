# cibadmin

`cibadmin` is a command-line utility used to manage the Cluster Information Base (CIB) in Pacemaker-based high-availability clusters. The CIB is a central XML-based database that stores the complete configuration and current state of the cluster, including nodes, resources, constraints, and other configuration parameters.



## Purpose

- **Configuration Management:**  
  `cibadmin` allows administrators to view, edit, and update the cluster configuration stored in the CIB. This is critical for applying new settings, modifying resources, or changing constraints.

- **Backup and Restore:**  
  The tool can be used to export the current CIB configuration to a file, making it possible to back up the configuration or compare changes over time. It also allows for restoring a previously saved CIB.

- **Diagnostics and Troubleshooting:**  
  By dumping the CIB content, administrators can review the exact configuration that the cluster manager is using, which aids in troubleshooting configuration-related issues.



## Basic Syntax

```bash
cibadmin [options]
```

`cibadmin` supports various options for querying, modifying, and saving the CIB configuration.



## Common Options and Usage

- **Dump the Current CIB Configuration:**
  ```bash
  cibadmin --query
  ```
  This command outputs the entire CIB configuration in XML format, allowing you to review all current cluster settings.

- **Export the CIB to a File:**
  ```bash
  cibadmin --query > /path/to/backup-cib.xml
  ```
  This exports the current configuration to a file for backup or further analysis.

- **Load a New CIB Configuration:**
  ```bash
  cibadmin --replace --xml-text="$(cat /path/to/new-cib.xml)"
  ```
  This command replaces the current CIB with the contents of the specified XML file.  
  **Warning:** Modifying the CIB can impact cluster behavior. Always back up the current CIB before making changes.

- **Validate the CIB Configuration:**
  Some versions of `cibadmin` may support options to check the syntax and consistency of the configuration before applying it, reducing the risk of errors.

- **Help and Version:**
  ```bash
  cibadmin --help
  cibadmin --version
  ```



## Example Workflow

1. **Backup the Current CIB:**
   ```bash
   cibadmin --query > /root/backup-cib.xml
   ```
   This creates a backup file of the current cluster configuration.

2. **Review or Edit the CIB:**
   Open the backup file in your preferred XML editor to review or modify the configuration as needed.

3. **Apply a New Configuration:**
   ```bash
   cibadmin --replace --xml-text="$(cat /root/new-cib.xml)"
   ```
   Replace the current CIB with your new configuration. Be cautious with this operation, as errors in the configuration may cause resource disruption.



## Best Practices

- **Always Backup First:**  
  Before making any changes to the CIB, use `cibadmin --query` to back up the current configuration.

- **Test Changes in a Staging Environment:**  
  If possible, validate configuration changes in a test environment or use simulation tools (like `crm_simulate`) to ensure that the new settings behave as expected.

- **Validate XML Syntax:**  
  Since the CIB is XML-based, ensure that any modifications result in valid XML. This helps prevent parsing errors when the configuration is applied.

- **Use Version Control:**  
  Consider storing your CIB backups and configuration files in version control to track changes over time and quickly revert if needed.



## Conclusion

`cibadmin` is an essential tool for managing the configuration of Pacemaker clusters. It provides the ability to query, back up, modify, and restore the Cluster Information Base, making it a critical component for cluster administrators. With careful use and adherence to best practices, `cibadmin` enables safe and effective management of cluster configurations, contributing to the overall stability and high availability of critical systems.

