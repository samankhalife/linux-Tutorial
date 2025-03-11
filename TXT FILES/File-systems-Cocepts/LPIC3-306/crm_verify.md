# crm_verify

`crm_verify` is a command-line utility from the crmsh (Cluster Resource Manager Shell) toolkit used in Pacemaker-based clusters. Its primary purpose is to validate cluster configurations—typically the XML Cluster Information Base (CIB) file—to ensure that they are syntactically correct and consistent with the rules and constraints expected by Pacemaker.



## Purpose

- **Configuration Validation:**  
  `crm_verify` checks the cluster configuration (usually in XML format) for syntax errors and structural inconsistencies before it is applied. This helps catch errors that could lead to resource failures or cluster instability.

- **Troubleshooting:**  
  By running `crm_verify`, administrators can identify misconfigurations or potential issues in the CIB. The tool provides diagnostic output that highlights errors and warnings, enabling corrective action before deployment.

- **Pre-Deployment Check:**  
  Verifying the configuration with `crm_verify` before pushing changes to a live cluster can prevent downtime and ensure that the configuration meets all required standards.



## Basic Syntax

```bash
crm_verify [options] [configuration-file]
```

- **configuration-file:**  
  If provided, `crm_verify` will validate the specified XML file. If omitted, it may validate the currently active cluster configuration stored in the CIB.



## Common Options

- **`-v` or `--verbose`:**  
  Produce detailed output, which is useful for diagnosing problems in the configuration.

- **`--strict`:**  
  Enable strict mode where warnings are treated as errors, ensuring a higher level of compliance with expected configuration standards.



## Example Usage

1. **Verify an XML Configuration File:**
   ```bash
   crm_verify /path/to/cib.xml
   ```
   This command checks the specified CIB file for any syntax or consistency errors.

2. **Verbose Verification:**
   ```bash
   crm_verify -v /etc/cib.xml
   ```
   This provides a more detailed diagnostic output, useful for pinpointing specific issues in the configuration.

3. **Validate Active Configuration:**
   Running `crm_verify` without specifying a file may check the active configuration in the cluster’s CIB, depending on your environment’s setup.



## Conclusion

`crm_verify` is a valuable tool for administrators managing Pacemaker clusters. By verifying that the cluster configuration is error-free and consistent, it helps prevent misconfigurations that could lead to service disruption. Running this tool before applying configuration changes is a best practice to ensure high availability and smooth cluster operations.
