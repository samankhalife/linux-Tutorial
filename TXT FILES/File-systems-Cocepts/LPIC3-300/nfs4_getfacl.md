# nfs4_getfacl

`nfs4_getfacl` is a command-line utility used to display the Access Control Lists (ACLs) of files and directories on NFSv4-mounted filesystems. ACLs provide more granular permission control than traditional UNIX file permissions, allowing detailed specifications of who can access files or directories and what operations they are permitted to perform.

This tool is typically used in environments where NFSv4 is employed, and administrators need to view or verify the ACLs to ensure the correct permissions are applied.

## Purpose

- **Display NFSv4 ACLs**:  
  `nfs4_getfacl` shows the current ACLs of files and directories in an NFSv4-mounted environment. It allows administrators to check who has access and what actions they can perform (read, write, execute).

- **Verify Permission Settings**:  
  Helps system administrators verify that access control is set correctly and matches the intended security policies.

## Basic Syntax

```bash
nfs4_getfacl [OPTIONS] <FILE>
```

- **`<FILE>`**: The file or directory whose ACLs will be displayed.

## Common Options

- **`-a`**:  
  Show all ACL entries (including special entries like owner and group).
  ```bash
  nfs4_getfacl -a file.txt
  ```

- **`-n`**:  
  Display the ACL in a numeric format, showing the underlying numeric values for the permissions and IDs.
  ```bash
  nfs4_getfacl -n file.txt
  ```

- **`-d`**:  
  Display the default ACL entries for a directory.
  ```bash
  nfs4_getfacl -d directory
  ```

- **`--help`**:  
  Show help information about the command.

## Example Usage

1. **Displaying ACL of a File**
   ```bash
   nfs4_getfacl file.txt
   ```
   This command displays the current ACL of `file.txt`, showing who has access and their specific permissions.

2. **Displaying ACL in Numeric Format**
   ```bash
   nfs4_getfacl -n file.txt
   ```
   This command shows the ACL in numeric form, revealing the raw numeric representation of the user and group permissions.

3. **Showing Default ACL of a Directory**
   ```bash
   nfs4_getfacl -d /shared
   ```
   This command displays the default ACL for the `/shared` directory. Default ACLs are applied to new files or directories created within the directory.

4. **Displaying All ACL Entries for a File**
   ```bash
   nfs4_getfacl -a file.txt
   ```
   This command displays all ACL entries, including special entries such as owner, group, and others.

## Best Practices

- **Regular ACL Review**:  
  Periodically review ACLs to ensure that they align with your organization’s security policies. Over time, as user roles change, permissions may need to be updated.

- **Test Permissions**:  
  After reviewing ACLs, test file and directory access from the perspective of different users and groups to ensure that the permissions are functioning as expected.

- **Use `nfs4_getfacl` Before Modifying ACLs**:  
  Always check the existing ACL using `nfs4_getfacl` before making changes with `nfs4_setfacl`. This helps avoid unintended permission modifications.

## Conclusion

`nfs4_getfacl` is a crucial tool for inspecting the current access control settings of files and directories in NFSv4 environments. By allowing administrators to view detailed ACLs, it helps ensure that permission configurations are correct, enhancing both security and operational control.
