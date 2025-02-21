# inherit-acls

`inherit-acls` is a Samba configuration parameter that determines whether new files and directories created on a Samba share inherit the Access Control Lists (ACLs) from their parent directory. Enabling this option ensures that permission settings defined on a folder are automatically applied to its contents, aligning Samba's behavior with that of Windows file systems.

## Purpose

- **Automatic ACL Inheritance**:  
  Ensures that when users create files or directories, the permissions (ACLs) set on the parent directory are automatically inherited by the new objects.

- **Consistency**:  
  Maintains uniform security settings across all files and directories in a share, reducing the administrative overhead of manually setting permissions on each new file or directory.

## Configuration

The `inherit-acls` parameter can be configured in the Samba configuration file (`smb.conf`), either globally or per share. The syntax is straightforward:

### Global Example
```ini
[global]
   inherit acls = yes
```

### Share-Specific Example
```ini
[share]
   path = /srv/samba/share
   read only = no
   inherit acls = yes
```

- **`yes`**: New files and directories will inherit ACLs from their parent.
- **`no`**: Inheritance is disabled; new objects will not automatically receive parent ACLs.

## How It Works

- **Inheritance Mechanism**:  
  When a user creates a new file or directory, Samba checks the ACLs of the parent directory. If `inherit-acls` is enabled, Samba applies the parent directory’s ACL settings to the new file or directory, subject to any modifications defined by other settings (such as `force create mode` or `force directory mode`).

- **Integration with VFS Modules**:  
  The `inherit acls` setting often works alongside VFS ACL modules (like `vfs_acl_xattr` or `vfs_acl_tdb`) to ensure that ACL data is stored either in extended attributes or in a TDB file, respectively.

## Use Cases

- **Enterprise Environments**:  
  Ensures that all users have consistent permissions on shared directories, which is critical in organizations that enforce strict security policies.

- **Mixed OS Networks**:  
  Provides Windows-like ACL inheritance on Samba shares, making it easier to integrate with Windows clients that expect inherited permissions.

- **Administrative Efficiency**:  
  Reduces the need to manually set ACLs on each file or directory created within a shared folder, streamlining file system management.

## Considerations

- **Filesystem Support**:  
  The underlying filesystem must support ACLs (e.g., ext4 with ACL support enabled, XFS, or Btrfs) for inheritance to work properly.

- **Testing**:  
  Test the setting on a small share to ensure that the inherited ACLs are applied as expected before rolling it out to a production environment.

- **Interaction with Other Settings**:  
  Review how `inherit-acls` interacts with other Samba settings related to permissions (e.g., `create mask`, `force create mode`) to avoid unexpected results.

## Conclusion

The `inherit-acls` parameter in Samba simplifies permission management by ensuring that new files and directories automatically receive ACLs from their parent directory. This feature is especially useful in mixed-OS and enterprise environments where consistent and secure access control is critical. Proper configuration and testing ensure that the inheritance behavior meets your organization’s security requirements.
