# smbcacls

`smbcacls` is a Samba command-line utility used to manage Windows NT-style Access Control Lists (ACLs) on files and directories in Samba shares. It provides functionality similar to Windows tools like `icacls` by allowing administrators to view, set, and copy ACLs. This helps ensure that permissions on files served by Samba match the intended security policies.

## Overview

- **View ACLs**: Display the current NT ACLs for a file or directory.
- **Set ACLs**: Modify or replace the NT ACL on a file or directory.
- **Copy ACLs**: Copy ACL settings from one file or directory to another.

## Basic Syntax

```bash
smbcacls [OPTIONS] //<server>/<share> <path> [ACL command] [parameters]
```

- **`<server>`**: The Samba server (hostname or IP).
- **`<share>`**: The name of the Samba share.
- **`<path>`**: The path within the share to the file or directory.
- **`ACL command`**: The specific operation (e.g., `--get`, `--set`, `--copy`).

## Common Subcommands

### get
**Purpose**: Retrieve and display the NT ACL for a specified file or directory.

**Usage**:
```bash
smbcacls //<server>/<share> <path> -U <username> --get
```

**Example**:
```bash
smbcacls //fileserver/public document.txt -U Administrator --get
```
This command displays the ACL for `document.txt` on the `public` share of `fileserver`.

---

### set
**Purpose**: Set or replace the NT ACL for a specified file or directory.

**Usage**:
```bash
smbcacls //<server>/<share> <path> -U <username> --set "<security_descriptor>"
```

**Example**:
```bash
smbcacls //fileserver/public document.txt -U Administrator --set "D:(A;;FA;;;S-1-5-21-123456789-123456789-123456789-1001)"
```
This command sets the ACL for `document.txt`, granting full access (FA) to the specified SID.

---

### copy
**Purpose**: Copy the NT ACL from one file or directory to another.

**Usage**:
```bash
smbcacls //<server>/<share> <source_path> -U <username> --copy <destination_path>
```

**Example**:
```bash
smbcacls //fileserver/public folder1/file.txt -U Administrator --copy folder2/file.txt
```
This copies the ACL from `folder1/file.txt` to `folder2/file.txt`.

---

## Additional Options

- **`-U <username>`**: Specifies the user for authentication.
- **`--verbose`**: Enables detailed output for better insight into the operations.
- **`-d` or `--debug`**: Increases debug output, useful for troubleshooting.
- **`--help`**: Displays usage information and available options.

## Use Cases

- **Permission Auditing**:  
  Quickly review file and directory ACLs to verify that permissions are set as intended.

- **Automated ACL Management**:  
  Integrate `smbcacls` into scripts to enforce consistent ACL settings across multiple files or shares.

- **Migration and Backup**:  
  Preserve file security settings by copying ACLs from original files to backup or migrated files.

## Conclusion

`smbcacls` is an essential tool for Samba administrators who need to manage Windows NT-style ACLs on file shares. By offering subcommands to get, set, and copy ACLs, it helps maintain consistent and secure file permissions in mixed Windows/Unix environments. Whether used interactively or integrated into automated scripts, `smbcacls` plays a key role in ensuring that file security policies are properly enforced.

