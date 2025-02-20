# setfacl

`setfacl` is a Linux command-line utility used to set Access Control Lists (ACLs) on files and directories. ACLs allow for more granular permission management than the traditional Unix file permission model, enabling you to assign specific permissions to multiple users and groups.

## Overview

- **Purpose**:  
  To modify and manage extended file permissions on filesystems that support ACLs, providing finer control over access beyond standard owner, group, and other permissions.

- **Usage Context**:  
  Typically used on filesystems like ext4, XFS, or Btrfs that support extended attributes (xattrs), allowing you to enforce detailed security policies.

## Basic Syntax

```bash
setfacl [OPTIONS] [ACL_ENTRIES] FILE...
```

- **OPTIONS**: Command-line flags to control behavior.
- **ACL_ENTRIES**: Entries defining the ACL modifications.
- **FILE...**: One or more files or directories to which the ACL settings are applied.

## Common Options

- **`-m, --modify`**:  
  Modify the ACL by adding or updating entries.  
  _Example_:  
  ```bash
  setfacl -m u:alice:rw file.txt
  ```
  Grants user `alice` read and write permissions on `file.txt`.

- **`-x, --remove`**:  
  Remove a specific ACL entry.  
  _Example_:  
  ```bash
  setfacl -x u:alice file.txt
  ```
  Removes any ACL entry for `alice` from `file.txt`.

- **`-b, --remove-all`**:  
  Remove all ACL entries from a file, reverting to standard Unix permissions.  
  _Example_:  
  ```bash
  setfacl -b file.txt
  ```

- **`-R, --recursive`**:  
  Apply ACL changes recursively to all files and directories within a directory.  
  _Example_:  
  ```bash
  setfacl -R -m u:alice:rw /shared
  ```

- **`-k, --remove-default`**:  
  Remove default ACL entries from a file or directory.  
  _Example_:  
  ```bash
  setfacl -k file.txt
  ```

## Examples

### 1. Granting Permissions to a User

Grant user `alice` read and write permissions on `document.txt`:
```bash
setfacl -m u:alice:rw document.txt
```

### 2. Removing a User’s ACL Entry

Remove any ACL entry for user `alice` from `document.txt`:
```bash
setfacl -x u:alice document.txt
```

### 3. Setting Default ACLs on a Directory

Set default ACLs so that every new file in `/shared` grants user `bob` read and write permissions:
```bash
setfacl -m d:u:bob:rw /shared
```
(The `d:` prefix specifies a default ACL for newly created files/directories within `/shared`.)

### 4. Removing All ACLs

Clear all ACL entries from `document.txt`, reverting to standard permissions:
```bash
setfacl -b document.txt
```

### 5. Recursively Setting ACLs

Recursively grant user `charlie` execute permission on all files and directories in `/scripts`:
```bash
setfacl -R -m u:charlie:x /scripts
```

## Best Practices

- **Backup ACLs**:  
  Use `getfacl` to back up current ACL settings before making changes:
  ```bash
  getfacl file.txt > file.txt.acl
  ```

- **Test on a Small Scale**:  
  Apply changes to a test file or directory first to ensure they have the desired effect.

- **Understand the ACL Mask**:  
  The ACL mask can limit the effective permissions. Verify settings using `getfacl` to see the impact of the mask.

- **Use Recursive Changes Cautiously**:  
  When using the `-R` option, ensure that the intended permissions are applied correctly to avoid unintended permission modifications.

## Conclusion

`setfacl` provides a powerful way to manage file and directory permissions with greater precision than traditional Unix permissions. By allowing you to set detailed ACLs, it ensures that specific users and groups have the appropriate level of access, which is especially useful in complex environments or when integrating with systems that require fine-grained security control.
