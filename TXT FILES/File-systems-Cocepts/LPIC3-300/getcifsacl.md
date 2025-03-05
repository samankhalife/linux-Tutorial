# getcifsacl

`getcifsacl` is a command-line utility that retrieves and displays the Access Control Lists (ACLs) for files and directories mounted via CIFS (Common Internet File System). This tool is particularly useful for inspecting the detailed permission settings on files and directories shared via Windows-based file shares or Samba.

## Purpose

- **Retrieve CIFS ACLs**:  
  The `getcifsacl` command allows administrators to query and display the ACL entries associated with a file or directory on a CIFS mount.
  
- **View Permission Details**:  
  It provides an easy way to inspect the fine-grained permissions (e.g., read, write, execute) that have been applied, in the context of Windows ACL formats.
  
- **Troubleshoot Permission Issues**:  
  By displaying the ACLs, administrators can diagnose permission-related issues on shared files and directories.

## Basic Syntax

```bash
getcifsacl [options] <file_or_directory>
```

- **`<file_or_directory>`**:  
  The path to the target file or directory on the CIFS mount.

## Common Options

- **`-h, --help`**:  
  Display help and usage information.

- **`-v, --verbose`**:  
  Provide more detailed output when querying ACL information.

## Example Usage

1. **Retrieve the ACL of a File**

   To retrieve and display the ACL entries for a file located on a CIFS mount:
   ```bash
   getcifsacl /mnt/cifs/share/document.txt
   ```

   Example Output:
   ```bash
   REVISION:1
   OWNER:BUILTIN\Administrators
   GROUP:BUILTIN\Users
   ACL:BUILTIN\Administrators:ALLOWED/OI|CI/FULL
   ACL:DOMAIN\user1:ALLOWED/READ
   ```

2. **Retrieve the ACL of a Directory**

   To display the ACL for a directory:
   ```bash
   getcifsacl /mnt/cifs/share/folder
   ```

## Interpreting the Output

The output of `getcifsacl` consists of several key fields:

- **REVISION**:  
  The ACL revision level (typically `1`).
  
- **OWNER**:  
  The owner of the file or directory.
  
- **GROUP**:  
  The primary group associated with the file or directory.
  
- **ACL Entries**:  
  These lines represent individual Access Control Entries (ACEs). They specify who (user or group) has which permissions (e.g., `FULL`, `READ`, `WRITE`). Flags like `OI` (Object Inherit) and `CI` (Container Inherit) define how permissions are propagated to subfiles and subdirectories.

## Best Practices

- **Regular Monitoring**:  
  Use `getcifsacl` regularly to check and audit the ACLs on critical shared files and directories.

- **Compare Before and After Changes**:  
  If you're modifying ACLs using `setcifsacl`, always retrieve the ACLs before and after the change to verify that the correct permissions are applied.

- **Combine with `setcifsacl`**:  
  Use `getcifsacl` to first retrieve the ACL of a file or directory, then use `setcifsacl` to modify the ACL as needed.


## Conclusion

`getcifsacl` is an invaluable tool for administrators managing CIFS-mounted shares. It allows the retrieval and inspection of Windows NT-style ACLs, providing clear visibility into who has access to which files and directories. This utility is essential for auditing and troubleshooting access permissions in mixed Linux and Windows environments.
