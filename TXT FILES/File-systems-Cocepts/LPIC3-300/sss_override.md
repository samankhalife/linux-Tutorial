# sss_override

`sss_override` is a command-line utility provided by SSSD (System Security Services Daemon) that allows administrators to manually override or inject custom entries into SSSD’s cache. This tool is particularly useful for testing, troubleshooting, and temporarily modifying the behavior of SSSD without requiring changes to the underlying remote identity source (such as LDAP or Active Directory).

## Purpose

- **Testing and Troubleshooting**:  
  Allows you to simulate user, group, or host entries to verify system behavior, troubleshoot authentication issues, or test configuration changes without impacting the live directory data.

- **Temporary Overrides**:  
  Enables temporary modifications to identity lookups. For example, you can force SSSD to return a specific UID/GID for a given username, regardless of the actual data from the remote source.

- **Development**:  
  Developers can use `sss_override` to test applications that rely on SSSD for identity information by injecting controlled data into the cache.

## Basic Syntax

```bash
sss_override [OPTIONS] <command> [arguments]
```

### Common Commands

- **add**:  
  Inject a custom override into the SSSD cache.
  
  **Usage**:
  ```bash
  sss_override add <object_type> <object_identifier> [attributes...]
  ```
  **Example** (Override a user entry):
  ```bash
  sss_override add user alice --uid=12345 --gid=1000 --gecos="Test User" --home="/home/alice"
  ```
  This command creates an override for the user `alice` with the specified UID, GID, GECOS field, and home directory.

- **remove**:  
  Remove an existing override from the cache.
  
  **Usage**:
  ```bash
  sss_override remove <object_type> <object_identifier>
  ```
  **Example**:
  ```bash
  sss_override remove user alice
  ```
  This removes the override for the user `alice`, allowing SSSD to revert to its normal lookup process.

- **list**:  
  Display all active overrides currently applied in SSSD.
  
  **Usage**:
  ```bash
  sss_override list
  ```
  **Example**:
  ```bash
  sss_override list
  ```
  This command outputs a list of all custom overrides present in the SSSD cache.

- **help**:  
  Show help information for using `sss_override`.
  
  **Usage**:
  ```bash
  sss_override --help
  ```

## Use Cases

- **Simulating Identity Changes**:  
  Test how applications behave when user or group attributes are modified, without affecting the live directory.

- **Troubleshooting Authentication Issues**:  
  Override problematic user or group entries temporarily to isolate and diagnose authentication or lookup problems.

- **Development and Testing**:  
  Developers can inject test data into SSSD’s cache to simulate various identity scenarios in a controlled environment.

## Best Practices

- **Temporary Use**:  
  Use overrides only for short-term testing or troubleshooting. Remember to remove them once the issue is resolved.
  
- **Security**:  
  Since `sss_override` can alter identity data, restrict its usage to trusted administrators. Changes made through overrides can affect authentication and access control.

- **Documentation**:  
  Document any overrides applied during testing to ensure they are not left in place accidentally.

- **Monitor Logs**:  
  After applying an override, check SSSD logs (typically in `/var/log/sssd/`) to confirm that the override is being applied as expected and that it resolves the issue being tested.

## Conclusion

`sss_override` is a powerful tool for SSSD administrators and developers. It provides a mechanism to manually inject, modify, or remove identity data in SSSD’s cache, facilitating testing, troubleshooting, and temporary adjustments. By using `sss_override` carefully and in conjunction with proper logging and documentation, you can effectively simulate and resolve identity-related issues without impacting your live environment.
