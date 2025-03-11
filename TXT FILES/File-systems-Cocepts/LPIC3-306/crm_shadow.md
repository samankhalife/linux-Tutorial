# crm_shadow 
`crm_shadow` is a utility within the crmsh (Cluster Resource Manager Shell) toolkit used to work with a “shadow” copy of the cluster configuration (the CIB, or Cluster Information Base) in a Pacemaker-managed cluster. Although its usage is not as widely documented as some other crmsh commands, its primary functions generally include:

- **Backup:**  
  Creating a shadow copy of the current active configuration. This backup can serve as a point-in-time snapshot of the cluster’s settings, which is useful for change management or for recovering from misconfigurations.

- **Comparison:**  
  Comparing the current active CIB against a previously saved shadow copy. This helps administrators identify what changes have been made over time and can aid in troubleshooting configuration-related issues.

- **Restore:**  
  In some implementations, `crm_shadow` may provide functionality to restore the cluster configuration from a shadow copy. This can be valuable if a recent change leads to instability or if the active CIB becomes corrupted.

### Typical Operations

- **Save the Active CIB to a Shadow File:**  
  This operation creates a backup of the current configuration.
  ```bash
  crm_shadow --save /path/to/shadow-cib.xml
  ```
  *(Note: The actual flag or syntax might differ depending on the version of crmsh.)*

- **Compare a Shadow CIB with the Active Configuration:**  
  To display differences between the saved configuration and the current active one:
  ```bash
  crm_shadow --diff /path/to/shadow-cib.xml
  ```

- **Restore the CIB from a Shadow Copy:**  
  This operation would replace the active configuration with the saved one:
  ```bash
  crm_shadow --restore /path/to/shadow-cib.xml
  ```

### Considerations

- **Version Dependency:**  
  The availability and exact syntax of `crm_shadow` can vary depending on the crmsh version and distribution. It’s recommended to check the help output:
  ```bash
  crm_shadow --help
  ```
  for the specific options and usage supported in your environment.

- **Caution When Restoring:**  
  Because the CIB controls the cluster configuration, restoring from a shadow copy should be done with care—ideally after verifying that the shadow file is correct and tested in a non-production environment.

### Conclusion

While `crm_shadow` may not be as commonly used or documented as other crmsh commands like `crm_mon` or `crm_resource`, it plays a valuable role in cluster configuration management. By allowing administrators to create, compare, and potentially restore a shadow copy of the CIB, it provides an additional layer of safety and change control in managing Pacemaker clusters.

If you plan to use `crm_shadow`, be sure to consult your crmsh version’s help documentation and test its functionality in a controlled setting before relying on it in production.
