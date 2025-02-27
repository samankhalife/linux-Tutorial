# /etc/idmapd.conf

`/etc/idmapd.conf` is the main configuration file for the NFSv4 ID mapping daemon (rpc.idmapd). This daemon is responsible for translating NFSv4 user and group identifiers between the string format (e.g., "user@domain") and the local numeric UID/GID values used by the Unix/Linux system. Proper configuration of `idmapd.conf` is essential for ensuring that file ownership and permissions are correctly interpreted between NFSv4 clients and servers, especially in environments with heterogeneous identity domains.

## Overview

- **Purpose**:  
  `idmapd.conf` configures how the NFSv4 ID mapping service converts between the NFSv4 identity format and the local UID/GID. This is vital for maintaining consistent file access permissions on NFSv4-mounted filesystems.

- **Role in NFSv4**:  
  In NFSv4, file ownership is represented by strings (e.g., "alice@example.com"). The rpc.idmapd service uses the settings in `idmapd.conf` to map these strings to corresponding numeric IDs, allowing Unix-like systems to apply local filesystem permissions.

## Key Sections and Parameters

### [General] Section

This section contains global settings that apply to all domain mappings.

- **Verbosity and Logging**:  
  Options like `Verbosity` control the amount of debugging information that the daemon will log.
  ```ini
  [General]
  Verbosity = 0
  ```
  A higher value increases the debug output, useful for troubleshooting.

- **Domain**:  
  The default domain can be specified here, which will be appended to usernames that do not include an explicit domain.
  ```ini
  Domain = EXAMPLE.COM
  ```

### [Mapping] Section

This section defines how to translate names to UIDs/GIDs. Common parameters include:

- **Nobody-User and Nobody-Group**:  
  Specifies fallback user and group for unmapped identities.
  ```ini
  [Mapping]
  Nobody-User = nobody
  Nobody-Group = nogroup
  ```

- **Method**:  
  The mapping method can be set to determine how the conversion is handled. The default method is typically "nsswitch" based or can use a simple algorithm for local mappings.

### Other Considerations

- **Case Sensitivity**:  
  The configuration may affect how case differences in usernames are handled. It’s important that the domain name and mapping rules are consistent with your environment.

- **Integration with NFSv4**:  
  The settings in `idmapd.conf` must be coordinated with the NFSv4 server and client configuration to ensure that file ownership and permissions are correctly managed across systems.

## Example Configuration

Below is an example of a typical `/etc/idmapd.conf` file:

```ini
[General]
# The default realm to use for mapping
Domain = EXAMPLE.COM
# Set verbosity (0 = minimal, higher numbers for more debug output)
Verbosity = 0

[Mapping]
# Fallback user and group for unmapped identities
Nobody-User = nobody
Nobody-Group = nogroup

# Uncomment and adjust the following if using a specific mapping algorithm or range
# Method = rid
# Range = 10000-20000
```

In this example:
- The default domain is set to `EXAMPLE.COM`, so identities will be interpreted within that realm if no domain is specified.
- The fallback account is configured as `nobody/nogroup`, which is used when an identity cannot be mapped.
- Additional parameters (such as mapping method or UID/GID range) can be configured as needed for your environment.

## Best Practices

- **Secure the File**:  
  Since `idmapd.conf` contains configuration details critical for identity mapping, ensure that its permissions are set to be readable only by privileged users (typically 600).

- **Consistency Across Systems**:  
  In environments with multiple NFSv4 servers and clients, ensure that all systems use a consistent `idmapd.conf` configuration to avoid discrepancies in UID/GID mappings.

- **Testing**:  
  After modifying `idmapd.conf`, restart the rpc.idmapd service and verify mappings using tools like `nfsidmap` or by checking file ownership on NFS-mounted directories.

- **Documentation**:  
  Keep a record of your `idmapd.conf` configuration, especially if you have custom mapping rules, to help troubleshoot issues and maintain consistency in a multi-server environment.

## Conclusion

`/etc/idmapd.conf` is a key configuration file for managing NFSv4 ID mapping on Unix-like systems. By properly configuring the general and mapping sections, administrators ensure that user and group identities are consistently translated between the NFSv4 string format and local UID/GID values. This consistency is critical for maintaining proper file permissions and secure access control in environments that rely on NFSv4 for network file sharing.
