# corosync-cmapctl

`corosync-cmapctl` is a utility used to query and modify the runtime configuration map (cmap) of the Corosync cluster engine. The cmap holds dynamic parameters that govern various aspects of Corosync's behavior, such as logging settings, network parameters, and quorum settings. With this tool, administrators can inspect live configuration values and, when permitted, adjust them on the fly without restarting the Corosync service.

## Purpose

- **Inspect Runtime Configuration:**  
  View all current configuration keys and their values, which aids in monitoring the cluster’s operational state.

- **Dynamic Tuning:**  
  Adjust runtime parameters (e.g., change logging levels) to fine-tune performance or troubleshoot issues without a full restart.

- **Troubleshooting:**  
  Quickly diagnose issues by examining the live state of the Corosync configuration.

## Basic Syntax

```bash
corosync-cmapctl [key [value]]
```

- **No Arguments:**  
  Running `corosync-cmapctl` without arguments lists all configuration keys with their current runtime values.

- **Query a Specific Key:**  
  To view the value of a specific key:
  ```bash
  corosync-cmapctl <key>
  ```
  Example:
  ```bash
  corosync-cmapctl logging.file_level
  ```
  
- **Set a Key's Value:**  
  To change the value of a writable key:
  ```bash
  corosync-cmapctl <key> <new_value>
  ```
  Example:
  ```bash
  corosync-cmapctl logging.file_level DEBUG
  ```

## Common Use Cases

- **View Full Configuration:**  
  Running the tool without parameters provides an overview of all runtime settings.
  
- **Adjust Logging Verbosity:**  
  Quickly change the logging level (e.g., from INFO to DEBUG) to increase diagnostic output during troubleshooting.

- **Monitor Network Parameters:**  
  Check and adjust network-related settings that impact cluster communication.

## Best Practices

- **Check Write Permissions:**  
  Not all configuration keys are modifiable at runtime; verify that the key supports changes before modifying.

- **Caution with Changes:**  
  Altering runtime parameters can impact cluster stability. Test changes in a non-production environment if possible.

- **Documentation:**  
  Record any runtime changes made so that you can revert or further adjust settings if necessary.

## Conclusion

`corosync-cmapctl` provides administrators with a powerful interface to monitor and adjust the live configuration of a Corosync cluster. By using this tool, you can gain insight into the current state of your cluster’s parameters and make dynamic changes to optimize performance or troubleshoot issues without service interruptions.
