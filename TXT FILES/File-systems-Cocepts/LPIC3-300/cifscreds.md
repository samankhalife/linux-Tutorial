# cifscreds

`cifscreds` is a Linux command-line utility used to manage user credentials for accessing CIFS (Common Internet File System) network file systems, such as those mounted via SMB (Server Message Block). It allows users to add, update, and delete credentials (username and password) for CIFS network shares, which can be cached in the kernel for future authentication.

## Purpose

- **Manage Credentials for CIFS Mounts**:  
  `cifscreds` simplifies the process of managing credentials required to access CIFS network shares. This is particularly useful for shares requiring user authentication, such as those found on Windows servers or Samba shares.

- **Automate Authentication**:  
  Instead of entering credentials each time the share is accessed, users can cache their credentials, enabling automatic authentication when accessing the CIFS mount.

- **Kerberos Authentication Support**:  
  `cifscreds` also supports caching Kerberos tickets, which can be used for seamless authentication to CIFS mounts in Kerberos-enabled environments.

## Basic Syntax

```bash
cifscreds <command> [options] <target>
```

- **`<command>`**:  
  Specifies the operation to perform (add, clear, update, or clearall).
  
- **`<target>`**:  
  Specifies the CIFS server (hostname or IP address) or share for which the credentials are being managed.

## Common Commands

1. **Add Credentials**
   
   This command caches the credentials for a specified CIFS server or share:
   ```bash
   cifscreds add <target>
   ```
   The command prompts for the username and password.

2. **Update Credentials**
   
   This command updates the cached credentials for a specific CIFS server or share:
   ```bash
   cifscreds update <target>
   ```
   It will prompt for the new password.

3. **Clear Credentials**
   
   This command clears the cached credentials for a specific CIFS server or share:
   ```bash
   cifscreds clear <target>
   ```

4. **Clear All Credentials**
   
   This command clears all cached credentials in the kernel for CIFS mounts:
   ```bash
   cifscreds clearall
   ```

## Example Usage

1. **Add Credentials for a CIFS Share**

   To cache the credentials (username and password) for a share on `fileserver.company.com`:
   ```bash
   cifscreds add fileserver.company.com
   ```
   The command will prompt for a username and password.

2. **Update Credentials**

   If the password for the CIFS share has changed, you can update the cached credentials:
   ```bash
   cifscreds update fileserver.company.com
   ```

3. **Clear Credentials**

   To remove the cached credentials for a specific share:
   ```bash
   cifscreds clear fileserver.company.com
   ```

4. **Clear All Credentials**

   To remove all cached credentials from the kernel:
   ```bash
   cifscreds clearall
   ```

## Security Considerations

- **User-Specific**:  
  The cached credentials are stored in the kernel and are specific to the user who ran the `cifscreds` command. This ensures that credentials are not shared across users.

- **Password Prompt**:  
  The command prompts for passwords in a secure manner and does not expose them in the command line or shell history.

- **Time-Limited Caching**:  
  Depending on system configuration, credentials cached by `cifscreds` may have a time limit after which they expire. Re-authentication may be required once they expire.

## Use Cases

- **CIFS Network Mounts with Credentials**:  
  For users who frequently access CIFS shares that require authentication, `cifscreds` provides an efficient way to manage credentials without needing to store them in fstab or other configuration files.

- **Kerberos Environments**:  
  In networks using Kerberos, `cifscreds` can cache Kerberos tickets for CIFS shares, enabling transparent authentication across Kerberos-enabled CIFS/SMB servers.

## Conclusion

`cifscreds` is a powerful utility for managing CIFS share credentials in Linux. It allows for seamless and secure access to network shares by caching credentials, simplifying the authentication process for users who frequently interact with CIFS/SMB file systems. Whether for individual file access or large-scale network shares, `cifscreds` helps streamline the authentication process while maintaining secure handling of credentials.
