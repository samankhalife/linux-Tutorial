# nfs4_setfacl

`nfs4_setfacl` is a command-line utility used to modify the Access Control List (ACL) for files and directories on NFSv4-mounted filesystems. Unlike traditional UNIX file permissions, NFSv4 ACLs offer more granular control over who can access a file or directory, allowing administrators to define detailed rules based on users, groups, and permissions.

This tool is typically used in environments where NFSv4 is used for file sharing, and access control needs to be more flexible than traditional file permissions.

## Purpose

- **Manage NFSv4 ACLs**:  
  `nfs4_setfacl` allows you to set, modify, and manage ACLs on files and directories in NFSv4-mounted filesystems. These ACLs define who can access files and what actions they can perform (e.g., read, write, execute).

- **Granular Access Control**:  
  Provides more detailed control than traditional UNIX file permissions, allowing for permissions to be granted or denied to individual users and groups.

## Basic Syntax

```bash
nfs4_setfacl [OPTIONS] <ACL_SPEC> <FILE>
```

- **`<ACL_SPEC>`**: The ACL specification that defines the permissions (e.g., granting or revoking access).
- **`<FILE>`**: The file or directory to which the ACL will be applied.

## Common Options

- **`-a`**:  
  Add a new ACL entry to the file.
  ```bash
  nfs4_setfacl -a user::rwx file.txt
  ```

- **`-d`**:  
  Apply the ACL to the default entry of a directory (used for new files and directories created within the directory).
  ```bash
  nfs4_setfacl -d -a user::rwx directory
  ```

- **`-x`**:  
  Remove an ACL entry from a file.
  ```bash
  nfs4_setfacl -x user::rwx file.txt
  ```

- **`-m`**:  
  Modify an existing ACL entry.
  ```bash
  nfs4_setfacl -m user::rw- file.txt
  ```

- **`-R`**:  
  Apply the ACL recursively to all files and subdirectories within a directory.
  ```bash
  nfs4_setfacl -R -m user::rwx /shared
  ```

- **`-n`**:  
  Display the ACLs without modifying them (useful for verifying current settings).
  ```bash
  nfs4_setfacl -n file.txt
  ```

- **`--help`**:  
  Display help information about the command.

## Example Usage

1. **Granting Read, Write, and Execute Permissions to a User**
   ```bash
   nfs4_setfacl -a user:alice:rwx file.txt
   ```
   This command grants user `alice` full permissions (read, write, execute) on `file.txt`.

2. **Setting Default ACL for a Directory**
   ```bash
   nfs4_setfacl -d -a user::rwx /shared
   ```
   This command sets the default ACL for the `/shared` directory, ensuring that any new files or directories created within `/shared` will inherit read, write, and execute permissions for the owner.

3. **Removing an ACL Entry**
   ```bash
   nfs4_setfacl -x user::rwx file.txt
   ```
   This command removes the ACL entry for user `alice` on `file.txt`.

4. **Applying ACL Recursively**
   ```bash
   nfs4_setfacl -R -m group::r-- /project
   ```
   This command applies a read-only permission for all users in the group on all files and directories under `/project`.

5. **Displaying the Current ACL**
   ```bash
   nfs4_setfacl -n file.txt
   ```
   This command shows the current ACL settings on `file.txt`.

## Best Practices

- **Backup ACLs**:  
  Before modifying ACLs, it is recommended to backup the current ACL settings using `nfs4_getfacl` so you can restore them if needed.

- **Limit Recursion**:  
  When applying ACLs recursively with `-R`, ensure that the changes are needed for all files and directories within a path to prevent accidental permission changes.

- **Test ACLs**:  
  Always verify that the new ACLs work as expected by testing access from the relevant users or groups.

## Conclusion

`nfs4_setfacl` is a powerful tool for managing NFSv4 ACLs, providing detailed control over file and directory permissions in networked environments. By offering flexibility in how permissions are granted, modified, and removed, `nfs4_setfacl` enhances access control over NFSv4-mounted filesystems and allows system administrators to implement fine-grained security policies.
