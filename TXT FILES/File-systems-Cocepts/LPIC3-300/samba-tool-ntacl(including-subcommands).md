# samba-tool ntacl

`samba-tool ntacl` is a Samba utility that allows administrators to manage and manipulate NT-style Access Control Lists (ACLs) on files and directories. This tool is essential for environments that require fine-grained permission management similar to that of Windows systems. It enables you to view, set, modify, copy, or reset NT ACLs, thereby ensuring that file and directory security policies are correctly applied in a Samba environment.

## Overview

- **NT ACL Management**:  
  `samba-tool ntacl` provides command-line access to NT ACL operations, allowing administrators to work with Windows-like security descriptors on Linux filesystems.

- **Integration with Samba**:  
  The tool is integrated into Samba, making it useful for managing permissions on shares provided by a Samba Active Directory Domain Controller or a standalone Samba server.

- **Subcommand-Based Interface**:  
  The utility is organized into several subcommands, each dedicated to a specific NT ACL operation (e.g., show, set, modify, copy).

## Common Subcommands

### 1. show
- **Purpose**:  
  Display the current NT ACL for a specified file or directory.
- **Usage**:
  ```bash
  samba-tool ntacl show <path>
  ```
- **Example**:
  ```bash
  samba-tool ntacl show /srv/samba/share/documents
  ```
  This command shows the NT ACL (including permissions, inherited entries, etc.) for the `/srv/samba/share/documents` directory.

### 2. set
- **Purpose**:  
  Set or replace the NT ACL on a file or directory with a specified security descriptor.
- **Usage**:
  ```bash
  samba-tool ntacl set <path> "<security_descriptor>"
  ```
- **Example**:
  ```bash
  samba-tool ntacl set /srv/samba/share/documents "D:(A;;FA;;;S-1-5-21-123456789-123456789-123456789-1001)"
  ```
  This command sets a new NT ACL on the specified directory. The security descriptor here defines an Access Control Entry (ACE) that grants full access (FA) to a specific SID.

### 3. modify
- **Purpose**:  
  Modify specific aspects of the existing NT ACL on a file or directory without replacing the entire ACL.
- **Usage**:
  ```bash
  samba-tool ntacl modify <path> <modification_options>
  ```
- **Example**:
  ```bash
  samba-tool ntacl modify /srv/samba/share/documents --add "D:(A;;R;;;S-1-5-21-123456789-123456789-123456789-1002)"
  ```
  This command adds a new ACE that grants read access (R) to another SID to the existing ACL on the directory.

### 4. copy
- **Purpose**:  
  Copy the NT ACL from one file or directory to another.
- **Usage**:
  ```bash
  samba-tool ntacl copy <source_path> <destination_path>
  ```
- **Example**:
  ```bash
  samba-tool ntacl copy /srv/samba/share/documents /srv/samba/share/backup
  ```
  This command copies the ACL from `/srv/samba/share/documents` to `/srv/samba/share/backup`, ensuring consistent permissions.

### 5. reset
- **Purpose**:  
  Reset the NT ACL of a file or directory to a default or inherited state.
- **Usage**:
  ```bash
  samba-tool ntacl reset <path>
  ```
- **Example**:
  ```bash
  samba-tool ntacl reset /srv/samba/share/documents
  ```
  This command resets the ACL on the specified directory, often useful when permission issues or conflicts need to be resolved.

## Best Practices and Considerations

- **Backup Existing ACLs**:  
  Before making changes with `samba-tool ntacl`, it is a good idea to back up the current ACL using the `show` subcommand. This allows you to restore settings if necessary.

- **Test in a Controlled Environment**:  
  When modifying NT ACLs, test your changes on non-critical files or directories to ensure that the security descriptors behave as expected.

- **Understanding Security Descriptors**:  
  Familiarize yourself with the syntax and structure of NT security descriptors (SIDs, ACEs, DACLs, etc.) to effectively use the `set` and `modify` subcommands.

- **Script Integration**:  
  The command-line nature of `samba-tool ntacl` makes it suitable for scripting and automated permission management. Ensure that your scripts handle error checking and logging appropriately.

## Conclusion

The `samba-tool ntacl` utility is an essential component for managing NT-style ACLs in Samba environments. With subcommands like `show`, `set`, `modify`, `copy`, and `reset`, it provides comprehensive tools for administrators to view and control file and directory permissions. Proper use of these commands helps maintain a secure and well-organized permission structure, critical for environments that rely on Windows-like security on Unix-based systems.
